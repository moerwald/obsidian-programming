
---
type: knowledge
---

[FluentValidation](https://github.com/FluentValidation/FluentValidation)

>A validation library for .NET that uses a fluent interface and lambda expressions for building strongly-typed validation rules.

## Example

```CSharp
using FluentValidation;

public class CustomerValidator: AbstractValidator<Customer> {
  public CustomerValidator() {
    RuleFor(x => x.Surname).NotEmpty();
    RuleFor(x => x.Forename).NotEmpty().WithMessage("Please specify a first name");
    RuleFor(x => x.Discount).NotEqual(0).When(x => x.HasDiscount);
    RuleFor(x => x.Address).Length(20, 250);
    RuleFor(x => x.Postcode).Must(BeAValidPostcode).WithMessage("Please specify a valid postcode");
  }

  private bool BeAValidPostcode(string postcode) {
    // custom postcode validating logic goes here
  }
}

var customer = new Customer();
var validator = new CustomerValidator();

// Execute the validator
ValidationResult results = validator.Validate(customer);

// Inspect any validation failures.
bool success = results.IsValid;
List<ValidationFailure> failures = results.Errors;
```


#DotNet 
#CSharp 