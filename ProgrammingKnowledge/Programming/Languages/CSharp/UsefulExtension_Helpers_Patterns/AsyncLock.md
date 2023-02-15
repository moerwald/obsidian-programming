
---
type: knowledge

---

Ein Lock das sowohl synchron als auch asynchron verwendet werden kann.



```CSharp

    public class AsyncLock
    {
        // Although SempaphoreSlim is disposable it does not need to be disposed in this context since we can control its usage.
        // See this for further explanation: https://stackoverflow.com/a/39195920/6682181
        private readonly SemaphoreSlim _semaphore = new SemaphoreSlim(1, 1);
        private readonly SemaphoreSlimReleaser _semaphoreReleaser;

        public AsyncLock() =>
            _semaphoreReleaser = new SemaphoreSlimReleaser(_semaphore);

        public IDisposable Acquire()
        {
            _semaphore.Wait();
            return _semaphoreReleaser;
        }

        /// <summary>
        /// This must be used in the following way: using (await _lock.AcquireAsync())
        /// If this call isn't awaited here, there won't be a compile error (because a Task is also IDisposable) but the locking will not work correctly.
        /// </summary>
        public async Task<IDisposable> AcquireAsync(CancellationToken cancellationToken = default)
        {
            await _semaphore.WaitAsync(cancellationToken).ConfigureAwait(false);
            return _semaphoreReleaser;
        }

        private class SemaphoreSlimReleaser : IDisposable
        {
            private readonly SemaphoreSlim _semaphore;

            public SemaphoreSlimReleaser(SemaphoreSlim semaphore) =>
                _semaphore = semaphore;

            public void Dispose() =>
                _semaphore.Release();
        }
    }
}



```

#Multithreading
#DotNet 
#CSharp 
#Helper 