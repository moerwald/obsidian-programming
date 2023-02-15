
[Quelle](https://livebook.manning.com/book/functional-programming-in-c-sharp-second-edition/chapter-13/110)

Bei [[EventSourcing]] werden, im Gegensatz zu CRUD Ansätzen, Events in Datenbanken gespeichert, und **nicht** States. Da Benutzer allerdings mit Events relativ wenig anfangen, müssen diese in entsprechende Views konvertiert werden. Hierzu werden meistens zwei Server Applikationen verwedent:

- *Command Side* : Empfängt Commands vom Client, validiert diese und wandelt diese in `Events` um. Die dann in der DB gespeichert werden. **Reines Schreiben**.
- *Query Side*: Diese Applikation kümmert sich um die Konvertierung von Events zu ViewModels. **Reines Lesen**

Oben beschriebener Side-Split hat folgende Vorteile:

- Bessere `Skalierbarkeit`.
- Schreiben wird einfacher, da die App "theoretisch" alles über einen einzigen Worker schreiben kann.

Ein Event beeinflußt immer nur eine Entität. Events können auch andere Events triggern, die wiederum andere Entitäten beeinflussen.


## Beispiel (functional programming)

```CSharp
  
void Main()  
{    // Setup account    var es = new EventStore();    var accountId = Guid.NewGuid();  
  
    {        var createAccount = new CreatedAccount(accountId, DateTime.UtcNow, CurrencyCode.Euro);        var account = Account.Create(createAccount);        var e = new DepositedCash(accountId, DateTime.UtcNow, 10.0m, Guid.NewGuid());  
        account = account.Apply(e);  
        es.Save(e);  
  
        e = e with { Amount = 20.0m };  
        account = account.Apply(e);  
        es.Save(e);  
  
        account.Dump("Account is setup, and persistet");  
    }    "".Dump("Freeze Account");  
    {        var fc = new FreezeAccount(DateTime.UtcNow, accountId);        // Recreate state after some time        var account = Account.Create(new CreatedAccount(accountId, DateTime.UtcNow, CurrencyCode.Euro));        foreach (var e in es.GetEvents())  
        {  
            account = account.Apply(e);  
        }  
  
        account.Dump("Recreated from store");  
        account = account.Apply(fc.ToEvent());  
        es.Add(fc.ToEvent());  
  
        account.Dump("new event applied");  
  
    }        "".Dump("Transfer Money");  
    {        var c = new TransferMoney(DateTime.UtcNow, accountId, "John Doe", "Iban1", "Bic1", 15.0m, "Birthday Present");        // Recreate state after some time        var account = Account.Create(new CreatedAccount(accountId, DateTime.UtcNow, CurrencyCode.Euro));        foreach (var e in es.GetEvents())  
        {  
            account = account.Apply(e);  
        }  
  
        account.Dump("Recreated from store");  
        account = account.Apply(c.ToEvent());  
        es.Add(c.ToEvent());  
  
        account.Dump("new event applied");  
    }  
      
      
}  
  
public abstract record Command(DateTime Timestamp);public record FreezeAccount(DateTime Timestamp, Guid AccountId) : Command(Timestamp)  
{    public FrozenAccount ToEvent() => new(AccountId, Timestamp);  
}  
  
public record TransferMoney(    DateTime Timestamp,    Guid AccountId,    string Beneficiary,    string Iban,    string Bic,    decimal DebitedAmount,    string Reference  
  
) : Command(Timestamp)  
{    public DebitedTransfer ToEvent() => new(AccountId, Timestamp, Beneficiary, Iban, Bic, DebitedAmount, Reference);  
}  
  
public static Option<AccountState> From  
    (IEnumerable<Event> history)  
    => history.Match(  
        Empty:() => F.None,  
        Otherwise: (created, otherEvents) =>            F.Some(  
                otherEvents.Aggregate(  
                    seed: Account.Create((CreatedAccount)created),  
                    (state, evt) => state.Apply(evt)))  
            );  
  
public static class Account{    public static AccountState Create(CreatedAccount evt)  
        => new AccountState        (  
        Currency: evt.Currency,  
        Status: AccountStatus.Active  
        );    public static AccountState Apply(this AccountState acc, Event evt)  
    => evt switch    {        DepositedCash e  
            => acc with { Balance = acc.Balance + e.Amount },        DebitedTransfer e  
            => acc with { Balance = acc.Balance - e.DebitedAmount },        FrozenAccount            => acc with { Status = AccountStatus.Frozen },        _ => throw new NotImplementedException()  
  
    };  
}  
  
  
public enum AccountStatus  
{  
    Undef = 0,  
    Requested,  
    Active,  
    Frozen  
}  
  
public sealed record AccountState(    CurrencyCode Currency,    AccountStatus Status = AccountStatus.Requested,    decimal Balance = 0m,    decimal AllowedOverdraft = 0m  
);  
  
  
  
public enum CurrencyCode  
{  
    Undef = 0,  
    Dollar,  
    Euro,  
    Yen  
}  
  
// You can define other methods, fields, classes and namespaces here  
public abstract record Event(Guid EntityId, DateTime Timestamp);public record CreatedAccount(Guid EntityId, DateTime TimeStamp, CurrencyCode Currency) : Event(EntityId, TimeStamp);  
  
public record FrozenAccount(Guid EntityId, DateTime TimeStamp) : Event(EntityId, TimeStamp);  
  
public record DepositedCash(Guid EntityId, DateTime TimeStamp, decimal Amount, Guid BranchId) : Event(EntityId, TimeStamp);  
  
public record DebitedTransfer(   Guid EntityId,   DateTime Timestamp,   string Beneficiary,   string Iban,   string Bic,   decimal DebitedAmount,   string Reference  
)  
: Event(EntityId, Timestamp);  
  
  
  
public class EventStore : List<Event>  
{    public void Save(Event e) => Add(e);    public IEnumerable<Event> GetEvents() => this;  
}
```

#CQRS
#FunctionalProgramming