
Mit der [[TaskCompletationSource]] ist es möglich vorab einen Task zu erzeugen, dessen Result **nocht nicht** gesetzt ist. Somit kann ein Caller sich einen Task geben, während dessen Result später gesetzt wird (in einem anderen Thread zum Beispiel). Hier ein Beispielcode:

```CSharp
async Task Main()  
{    
    var utap = new UseTaskAsPromise<int>();    
    var tcs = new CancellationTokenSource();  

    // Result wird nach 10 Sekunden aus einem anderen Task gesetzt
    utap.PromiseIsDeliveredAfter(TimeSpan.FromSeconds(10), 42);

    var sw = Stopwatch.StartNew();    

    // Wir warten auf das Result
    var value = await utap.GetPromise(tcs.Token);  
    sw.Elapsed.Dump();  
    value.Dump();  
}

public class UseTaskAsPromise<T>  
{    
    private readonly TaskCompletionSource<T> _tcs = new (TaskCreationOptions.RunContinuationsAsynchronously);    
    public Task<T> GetPromise(CancellationToken token)  
    {  
	    // Falls der Token gecancelt wird, soll dies an die TCS weiter gegeben werden
        token.Register(() => _tcs.SetCanceled());        
        return _tcs.Task;  
    }
    
    public void PromiseIsDeliveredAfter(TimeSpan timespan, T value) =>        
        Task.Factory.StartNew(async () =>  
        {            
             await Task.Delay(timespan);  
            _tcs.TrySetResult(value);  
        });  
}
```

#Task 
#CSharp 
#DotNet 