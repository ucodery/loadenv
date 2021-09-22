# loadenv

Automatically load environment variables into structured Python data

Loadenv makes it easy to pull environment variables into your program. It centralizes and hides the
task of loading environment variables and asserting necessary variables are set, while assigning
default values for those that are not required.

Loaded variables are cast to python objects based on type annotations and stored as identifiers, not
strings. So typo bugs are easier to catch and names are easier to autocomplete. It does all this
during startup, making bad invocations quit as soon as possible and with a clear error message,
rather than deep in business logic from strange Exceptions.


## Getting Started

Define an `EnvEnum` where each member is named exactly as the environment variable you wish to
capture. It should be annotated with the type you would like the member to be. You will have to
assign some value to the member to actually create it. For required environment variable this value
does not matter; values such as `()` or `...` are good choices.

```python
from loadenv import EnvEnum


# values are taken from the environment when the class is created
class Secrets(EnvEnum):
    USERNAME: str = ()
    USERPASS: str = ()
    USERAPIKEY: str = ()


# later on
requests.post(prod, headers={"Authorization": f"TOK:{Secrets.USERAPIKEY}"})
```
