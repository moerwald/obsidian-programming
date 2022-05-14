# File Copy with Progress Bar
To implement File-Copy with progress bar use marshalling in combination with `CopyEx`. `CopyEx` has a progress callback ;-). 

Code: 

``` csharp





[SupportedOSPlatform("windows")]
public class NativeRemoteCopy 
{
   
    private enum CopyFileCallbackAction
    {
        Continue = 0,
        Cancel = 1,
        Stop = 2,
        Quiet = 3
    }

    [Flags]
    private enum CopyFileOptions
    {
        None = 0x0,
        FailIfDestinationExists = 0x1,
        Restartable = 0x2,
        AllowDecryptedDestination = 0x8,
        All = FailIfDestinationExists | Restartable | AllowDecryptedDestination
    }

    private class CopyProgressData
    {
        private readonly string _sourceFilePath;
        private readonly string _destinationHost;
        private readonly ICopyProgress? _callback;

        public CopyProgressData(string sourceFilePath, string destinationHost, ICopyProgress? callback)
        {
            _sourceFilePath = sourceFilePath;
            _destinationHost = destinationHost;
            _callback = callback;
        }

        public int CallbackHandler(
            long totalFileSize, long totalBytesTransferred,
            long streamSize, long streamBytesTransferred,
            int streamNumber, int callbackReason,
            IntPtr sourceFile, IntPtr destinationFile, IntPtr data)
        {
            _callback?.Progress(_destinationHost, _sourceFilePath,
                (double) totalBytesTransferred / totalFileSize * 100, totalBytesTransferred, totalFileSize);
            return (int) CopyFileCallbackAction.Continue;
        }
    }

    public async Task<IEnumerable<RemoteCopyResult>> CopyFileToAsync(
        List<RemoteSession> sessions,
        List<(string LocalFilePath, string RemoteFilePath)> pathFiles,
        ICopyProgress progress,
        CancellationToken token) =>
        await Task.WhenAll(sessions.Select(session =>
            CopyImpersonatedAsync(session, pathFiles, progress, PreCopyActionSendFile, token)).ToList());

    
    private Task<RemoteCopyResult> CopyImpersonatedAsync(
        RemoteSession session,
        List<(string LocalFilePath, string RemoteFilePath)> pathFiles,
        ICopyProgress copyProgress,
        Func<string, ICopyProgress, (string, string), (bool, string, string)> preCopyAction,
        CancellationToken token) =>
        Task.Run(() =>
        {
            var returnValue = NativeMethods.LogonUser(session.UserName, session.HostName, session.Password,
                NativeMethods.LOGON_TYPE_NEW_CREDENTIALS, NativeMethods.LOGON32_PROVIDER_DEFAULT,
                out var safeAccessTokenHandle);
            try
            {
                if (!returnValue)
                {
                    var errorMessage = GetErrorMessageFromLastError();
                    copyProgress.Error(session.HostName, string.Empty, errorMessage);
                    return new RemoteCopyResult(session.HostName, false, errorMessage);
                }

                var result = true;
                var errorText = new StringBuilder();

                // Note: if you want to run as unimpersonated, pass  
                //       'SafeAccessTokenHandle.InvalidHandle' instead of variable 'safeAccessTokenHandle'  
                WindowsIdentity.RunImpersonated(safeAccessTokenHandle,
                    () =>
                    {
                        foreach (var file in pathFiles)
                        {
                            var (preCopyActionResult, sourceFilePath, destinationFilePath) =
                                preCopyAction(session.HostName, copyProgress, file);
                            if (!preCopyActionResult)
                            {
                                result = false;
                                continue;
                            }

                            var copyResult = CopyFile(sourceFilePath, session.HostName, destinationFilePath,
                                CopyFileOptions.None, copyProgress);
                            if (!copyResult.ok)
                            {
                                result = false;
                                errorText.Append(copyResult.errorText).Append(". ");
                                copyProgress.Error(session.HostName, file.LocalFilePath, copyResult.errorText);
                            }
                        }
                    }
                );
                return new RemoteCopyResult(session.HostName, result, errorText.ToString());
            }
            finally
            {
                safeAccessTokenHandle.Close();
                safeAccessTokenHandle.Dispose();
            }
        }, token);

    private static (bool Result, string SourceFilePath, string DestinationFilePath) PreCopyActionSendFile(
        string hostName, ICopyProgress copyProgress, (string LocalFilePath, string RemoteFilePath) file)
    {
        var destinationFilePath = string.Empty;
        if (!File.Exists(file.LocalFilePath))
        {
            copyProgress.Error(hostName, file.LocalFilePath, "File doesn't exist");
            return (false, file.LocalFilePath, destinationFilePath);
        }

        destinationFilePath = $@"\\{hostName}\{file.RemoteFilePath.Replace(':', '$')}";
        var destinationFolder = Path.GetDirectoryName(destinationFilePath);
        if (!Directory.Exists(destinationFolder))
        {
            try
            {
                Directory.CreateDirectory(destinationFolder);
            }
            catch (Exception e)
            {
                copyProgress.Error(hostName, file.LocalFilePath, e.Message);
                return (false, file.LocalFilePath, destinationFilePath);
            }
        }

        return (true, file.LocalFilePath, destinationFilePath);
    }

    private static (bool Result, string SourceFilePath, string DestinationFilePath) PreCopyActionReceiveFile(
        string hostName, ICopyProgress copyProgress, (string LocalFilePath, string RemoteFilePath) file)
    {
        if (File.Exists(file.RemoteFilePath))
        {
            // Here we want to copy the remote file to the local file. So the remote file is the source.
            return (true, file.RemoteFilePath, file.LocalFilePath);
        }

        copyProgress.Error(hostName, file.RemoteFilePath, "File doesn't exist");
        return (false, string.Empty, string.Empty);
    }

    private static (bool ok, string errorText) CopyFile(string sourceFilePath, string hostName,
        string destinationFilePath,
        CopyFileOptions options, ICopyProgress? callback)
    {
        var cpr = callback == null
            ? null
            : new NativeMethods.CopyProgressRoutine(new CopyProgressData(sourceFilePath, hostName, callback)
                .CallbackHandler);

        if (File.Exists(destinationFilePath))
        {
            var sourceCheckSum = CheckSum.GetSHA256From(sourceFilePath);
            var destinationCheckSum = CheckSum.GetSHA256From(destinationFilePath);
            if (sourceCheckSum == destinationCheckSum)
            {
                var fi = new FileInfo(sourceFilePath);
                callback?.Progress(hostName, sourceFilePath, 100, fi.Length, fi.Length);
                return (true, "File already copied. SHA256 of source and destination are equal");
            }
        }

        var cancel = false;
        return NativeMethods.CopyFileEx(sourceFilePath, destinationFilePath, cpr, IntPtr.Zero, ref cancel,
            (int) options)
            ? (true, string.Empty)
            : (false, errorMessage: GetErrorMessageFromLastError());
    }

    private static string GetErrorMessageFromLastError() =>
        new Win32Exception(Marshal.GetLastWin32Error()).Message;

    private static string ToUncPath(string hostName, string filePath) =>
        $@"\\{hostName}\{filePath.Replace(':', '$')}";
}



