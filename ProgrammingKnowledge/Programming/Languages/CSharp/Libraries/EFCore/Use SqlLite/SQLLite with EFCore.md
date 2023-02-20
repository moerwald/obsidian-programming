
Um EFCore mit SQLLite zu verwenden muss man im [[DBContext]] die [[OnConfiguring]]-Methode wie folgt überladen:

```CSharp

    public class GroceryDbContext : DbContext
    {
        public GroceryDbContext(DbContextOptions<GroceryDbContext> options) : base(options)
        {
            var folder = Environment.SpecialFolder.LocalApplicationData;
            var path = Environment.GetFolderPath(folder);
            DbPath = Path.Join(path, "grocery.db");
        }

        public string DbPath { get; }

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            // Hier gibt man die Verwendung von SQLLite an!
            optionsBuilder.UseSqlite($"Data Source={DbPath}");
        }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<GroceryItem>().HasData(
                new GroceryItem () { ID=1, Name = "Item1", Description = "Description1", Quantity = 1},
                new GroceryItem () { ID=2, Name = "Item2", Description = "Description2", Quantity = 2},
                new GroceryItem () { ID=3, Name = "Item3", Description = "Description3", Quantity = 3},
                new GroceryItem () { ID=4, Name = "Item4", Description = "Description4", Quantity = 4}
            );
        }

        public DbSet<GroceryItem> Items { get; set; }
    }

```


Über [[OnModelCreating]] kann man auch ein Array an Seed-Data angeben, dass beim Anlegen der DB erzeugt wird.

Die DB kann dann über folgende Befehle initialisiert werden:

```PowerShell

dotnet tool install --global dotnet-ef
dotnet add package Microsoft.EntityFrameworkCore.Design
dotnet ef migrations add InitialCreate
dotnet ef database update
```


#EfCore
#SQLLite 