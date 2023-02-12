# this

This mechanism is dynamic. `this` is bound at runtime based on the four below stated rules.

Four **important** things about `this`.

1. Was the function call with the new keyword?
2. Was the function called with `bind` or `apply`? = explicit this binding
3. Was the function called via a containing/owning object? = implicit binding
4. DEFAULT: global object (except in strict mode, defaults to the `undefined` value)

![[four_rules_of_this_JS.png.png]]