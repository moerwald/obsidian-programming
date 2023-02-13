
---
type: knowledge
---

Zeitweise hat man APIs die kein `CancelationToken` entgegen nehmen. Um die APIs doch canceln zu können kann man folgende Extension-Methods auf `Task` definieren.

```CSharp

        public static async Task<bool> HasTimedOutAfterAsync(this Task task, TimeSpan timeout)
        {
            using (var cts = new CancellationTokenSource())
                if (await Task.WhenAny(task, Task.Delay(timeout, cts.Token)).ConfigureAwait(false) == task)
                {
                    cts.Cancel();
                    // To avoid awaiting a canceled task which would throw a TaskCanceledException.
                    if (!task.IsCanceled)
                        // We need to await the task a second time to re-throw any exception.
                        await task.ConfigureAwait(false);

                    return false;
                }
                else
                    return true;
        }

        /// <summary>
        /// Internally creates a TaskCompletionSource to react to a possible cancellation and await either this task or the actual running task.
        /// </summary>
        /// <param name="task">The task to stop awaiting if necessary.</param>
        /// <param name="cancellationToken">The <see cref="CancellationToken"/> to which to react.</param>
        /// <remarks>IMPORTANT: The running task is not actually canceled. It will continue its normal execution. Only the awaiting operation is cut short.</remarks>
        /// <returns>A task which completes once either the original task has completed or the <see cref="CancellationToken"/> was signaled.</returns>
        public static async Task MakeAwaitCancelable(this Task task, CancellationToken cancellationToken)
        {
            // The non-generic TaskCompletionSource is only available starting with .Net 5.
            var cancellationTaskSource = new TaskCompletionSource<bool>(TaskCreationOptions.RunContinuationsAsynchronously);
            using (cancellationToken.Register(() => cancellationTaskSource.TrySetCanceled()))
            {
                // The await is necessary because otherwise the CancellationTokenRegistration would be disposed when returning the Task.
                var completedTask = await Task.WhenAny(task, cancellationTaskSource.Task).ConfigureAwait(false);
                // If the canceled task was first the first to complete, we need to await it in order to get the TaskCanceledException.
                await completedTask.ConfigureAwait(false);
            }
        }

        /// <summary>
        /// Internally creates a TaskCompletionSource to react to a possible cancellation and await either this task or the actual running task.
        /// </summary>
        /// <typeparam name="T">The type which the running task returns.</typeparam>
        /// <param name="task">The task to stop awaiting if necessary.</param>
        /// <param name="cancellationToken">The <see cref="CancellationToken"/> to which to react.</param>
        /// <remarks>IMPORTANT: The running task is not actually canceled. It will continue its normal execution. Only the awaiting operation is cut short.</remarks>
        /// <returns>A task which completes once either the original task has completed or the <see cref="CancellationToken"/> was signaled.</returns>
        public static async Task<T> MakeAwaitCancelable<T>(this Task<T> task, CancellationToken cancellationToken)
        {
            var cancellationTaskSource = new TaskCompletionSource<T>(TaskCreationOptions.RunContinuationsAsynchronously);
            using (cancellationToken.Register(() => cancellationTaskSource.TrySetCanceled()))
            {
                // The await is necessary because otherwise the CancellationTokenRegistration would be disposed when returning the Task.
                var completedTask = await Task.WhenAny(task, cancellationTaskSource.Task).ConfigureAwait(false);
                return await completedTask.ConfigureAwait(false);
            }
        }

```


#Task
#Cancel
#CSharp 
#DotNet