Eine Library die es ermöglicht Dummy Data zu generieren. Man hat bei [[Unit Tests]] oft das Problem Datenobjekte, bei denen der Inhalt unwichtig ist, aufzusetzen. Genau diesen Job übernimmt [[Bogus]], welches [hier](https://github.com/bchavez/Bogus) zu finden ist.

Hier ein kurzes Code Sample:

```CSharp

public enum Gender
{
    Male,
    Female
}

//Set the randomizer seed if you wish to generate repeatable data sets.
Randomizer.Seed = new Random(8675309);

var fruit = new[] { "apple", "banana", "orange", "strawberry", "kiwi" };

var orderIds = 0;
var testOrders = new Faker<Order>()
    //Ensure all properties have rules. By default, StrictMode is false
    //Set a global policy by using Faker.DefaultStrictMode
    .StrictMode(true)
    //OrderId is deterministic
    .RuleFor(o => o.OrderId, f => orderIds++)
    //Pick some fruit from a basket
    .RuleFor(o => o.Item, f => f.PickRandom(fruit))
    //A random quantity from 1 to 10
    .RuleFor(o => o.Quantity, f => f.Random.Number(1, 10))
    //A nullable int? with 80% probability of being null.
    //The .OrNull extension is in the Bogus.Extensions namespace.
    .RuleFor(o => o.LotNumber, f => f.Random.Int(0, 100).OrNull(f, .8f));

```


#NuGet 
#CSharp 
#DotNet 
#UnitTest
