In EFCore können Tabellen via C# Klassen dargestellt werden:

```CSharp
    public record GroceryItem
    {
        [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
        public int ID { get; set; }
        public string Name { get; set; }
        public string Description{ get; set; }
        public int Quantity{ get; set; }
    }


```

Wichtig ist folgendes:

- CTOR **OHNE** Parameter
- Properties haben public `get`,`set` -Methods


#Entity
#EfCore 