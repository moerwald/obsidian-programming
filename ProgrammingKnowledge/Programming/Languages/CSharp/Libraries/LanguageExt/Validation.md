
---
type: knowledge
---

Ein einfaches Beispiel wie man den [[Validation]] Monad verwenden kann:

```CSharp


    public class Person
    {
        public string Name { get; set; }
        public int Age { get; set; }
    }
    
    public static class PersonValidator
    {
        public static Validation<Error, Person> Validate(Person person)
        {
            return from name in ValidateName(person.Name)
                   from age in ValidateAge(person.Age)
                   select new Person { Name = name, Age = age };
        }
    
        private static Validation<Error, string> ValidateName(string name)
        {
            return name switch
            {
                null => Error.New("Name cannot be null"),
                "" => Error.New("Name cannot be empty"),
                _ => name
            };
        }
    
        private static Validation<Error, int> ValidateAge(int age)
        {
            return age switch
            {
                0 => Error.New("Age cannot be negative"),
                _ => age
            };
        }
    }
    
    public static void Main()
    {
        var validPerson = new Person { Name = "Alice", Age = 30 };
        var invalidPerson = new Person { Name = null, Age = -10 };
        Console.WriteLine($"Valid Person: {PersonValidator.Validate(validPerson)}");
        Console.WriteLine($"Invalid Person: {PersonValidator.Validate(invalidPerson)}");
    }
    
    public class Error
    {
        public string Message { get; }
        private Error(string message)
        {
            Message = message;
        }
        public static Error New(string message)
        {
            return new Error(message);
        }
    }

```

#Validation
#CSharp 
#DotNet 