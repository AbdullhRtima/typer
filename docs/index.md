<p align="center">
  <a href="https://typer.tiangolo.com"><img src="https://typer.tiangolo.com/img/logo-margin/logo-margin-vector.svg" alt="Typer"></a>
</p>
<p align="center">
    <em>Typer, build great CLIs. Easy to code. Based on Python type hints.</em>
</p>
<p align="center">
<a href="https://github.com/tiangolo/typer/actions?query=workflow%3ATest" target="_blank">
    <img src="https://github.com/tiangolo/typer/workflows/Test/badge.svg" alt="Test">
</a>
<a href="https://github.com/tiangolo/typer/actions?query=workflow%3APublish" target="_blank">
    <img src="https://github.com/tiangolo/typer/workflows/Publish/badge.svg" alt="Publish">
</a>
<a href="https://codecov.io/gh/tiangolo/typer" target="_blank">
    <img src="https://img.shields.io/codecov/c/github/tiangolo/typer?color=%2334D058" alt="Coverage">
</a>
<a href="https://pypi.org/project/typer" target="_blank">
    <img src="https://img.shields.io/pypi/v/typer?color=%2334D058&label=pypi%20package" alt="Package version">
</a>
</p>

---

**Documentation**: <a href="https://typer.tiangolo.com" target="_blank">https://typer.tiangolo.com</a>

**Source Code**: <a href="https://github.com/tiangolo/typer" target="_blank">https://github.com/tiangolo/typer</a>

---

Typer is a library for building <abbr title="command line interface, programs executed from a terminal">CLI</abbr> applications that users will **love using** and developers will **love creating**. Based on Python 3.6+ type hints.

The key features are:

* **Intuitive to write**: Great editor support. <abbr title="also known as auto-complete, autocompletion, IntelliSense">Completion</abbr> everywhere. Less time debugging. Designed to be easy to use and learn. Less time reading docs.
* **Easy to use**: It's easy to use for the final users. Automatic help, and automatic completion for all shells.
* **Short**: Minimize code duplication. Multiple features from each parameter declaration. Fewer bugs.
* **Start simple**: The simplest example adds only 2 lines of code to your app: **1 import, 1 function call**.
* **Grow large**: Grow in complexity as much as you want, create arbitrarily complex trees of commands and groups of subcommands, with options and arguments.

## FastAPI of CLIs

<a href="https://fastapi.tiangolo.com" target="_blank"><img src="https://fastapi.tiangolo.com/img/logo-margin/logo-teal.png" style="width: 20%;"></a>

**Typer** is <a href="https://fastapi.tiangolo.com" class="external-link" target="_blank">FastAPI</a>'s little sibling.

And it's intended to be the FastAPI of CLIs.

## Requirements

Python 3.6+

**Typer** stands on the shoulders of a giant. Its only internal dependency is <a href="https://click.palletsprojects.com/" class="external-link" target="_blank">Click</a>.

## Installation

<div class="termy">

```console
$ pip install "typer[all]"
---> 100%
Successfully installed typer
```

</div>

**Note**: that will include <a href="https://rich.readthedocs.io/" class="external-link" target="_blank">Rich</a>. Rich is the recommended library to *display* information on the terminal, it is optional, but when installed, it's deeply integrated into **Typer** to display beautiful output.

## Example

### The absolute minimum

* Create a file `main.py` with:

```Python
import typer


def main(name: str):
    print(f"Hello {name}")


if __name__ == "__main__":
    typer.run(main)
```

### Run it

Run your application:

<div class="termy">

```console
// Run your application
$ python main.py

// You get a nice error, you are missing NAME
<font color="#F4BF75">Usage: </font>main.py [OPTIONS] NAME
<font color="#A5A5A1">Try </font><font color="#44919F">&apos;main.py </font><font color="#44919F"><b>--help</b></font><font color="#44919F">&apos;</font><font color="#A5A5A1"> for help.</font>
<font color="#F92672">╭─ Error ───────────────────────────────────────────╮</font>
<font color="#F92672">│</font> Missing argument &apos;NAME&apos;.                          <font color="#F92672">│</font>
<font color="#F92672">╰───────────────────────────────────────────────────╯</font>


// You get a --help for free
$ python main.py --help

<b> </b><font color="#F4BF75"><b>Usage: </b></font><b>main.py [OPTIONS] NAME                       </b>
<b>                                                     </b>
<font color="#A5A5A1">╭─ Arguments ───────────────────────────────────────╮</font>
<font color="#A5A5A1">│ </font><font color="#F92672">*</font>    name      <font color="#F4BF75"><b>TEXT</b></font>  [default: None] <font color="#A6194C">[required]</font>   │
<font color="#A5A5A1">╰───────────────────────────────────────────────────╯</font>
<font color="#A5A5A1">╭─ Options ─────────────────────────────────────────╮</font>
<font color="#A5A5A1">│ </font><font color="#A1EFE4"><b>--install-completion</b></font>          Install completion  │
<font color="#A5A5A1">│                               for the current     │</font>
<font color="#A5A5A1">│                               shell.              │</font>
<font color="#A5A5A1">│ </font><font color="#A1EFE4"><b>--show-completion</b></font>             Show completion for │
<font color="#A5A5A1">│                               the current shell,  │</font>
<font color="#A5A5A1">│                               to copy it or       │</font>
<font color="#A5A5A1">│                               customize the       │</font>
<font color="#A5A5A1">│                               installation.       │</font>
<font color="#A5A5A1">│ </font><font color="#A1EFE4"><b>--help</b></font>                        Show this message   │
<font color="#A5A5A1">│                               and exit.           │</font>
<font color="#A5A5A1">╰───────────────────────────────────────────────────╯</font>

// When you create a package you get ✨ auto-completion ✨ for free, installed with --install-completion

// Now pass the NAME argument
$ python main.py Camila

Hello Camila

// It works! 🎉
```

</div>

**Note**: auto-completion works when you create a Python package and run it with `--install-completion` or when you use <a href="https://typer.tiangolo.com/typer-cli/" class="internal-link" target="_blank">Typer CLI</a>.

## Example upgrade

This was the simplest example possible.

Now let's see one a bit more complex.

### An example with two subcommands

Modify the file `main.py`.

Create a `typer.Typer()` app, and create two subcommands with their parameters.

```Python hl_lines="3  6  11  20"
import typer

app = typer.Typer()


@app.command()
def hello(name: str):
    print(f"Hello {name}")


@app.command()
def goodbye(name: str, formal: bool = False):
    if formal:
        print(f"Goodbye Ms. {name}. Have a good day.")
    else:
        print(f"Bye {name}!")


if __name__ == "__main__":
    app()
```

And that will:

* Explicitly create a `typer.Typer` app.
    * The previous `typer.run` actually creates one implicitly for you.
* Add two subcommands with `@app.command()`.
* Execute the `app()` itself, as if it was a function (instead of `typer.run`).

### Run the upgraded example

Check the new help:

<div class="termy">

```console
$ python main.py --help

<b> </b><font color="#F4BF75"><b>Usage: </b></font><b>main.py [OPTIONS] COMMAND [ARGS]...          </b>
<b>                                                     </b>
<font color="#A5A5A1">╭─ Options ─────────────────────────────────────────╮</font>
<font color="#A5A5A1">│ </font><font color="#A1EFE4"><b>--install-completion</b></font>          Install completion  │
<font color="#A5A5A1">│                               for the current     │</font>
<font color="#A5A5A1">│                               shell.              │</font>
<font color="#A5A5A1">│ </font><font color="#A1EFE4"><b>--show-completion</b></font>             Show completion for │
<font color="#A5A5A1">│                               the current shell,  │</font>
<font color="#A5A5A1">│                               to copy it or       │</font>
<font color="#A5A5A1">│                               customize the       │</font>
<font color="#A5A5A1">│                               installation.       │</font>
<font color="#A5A5A1">│ </font><font color="#A1EFE4"><b>--help</b></font>                        Show this message   │
<font color="#A5A5A1">│                               and exit.           │</font>
<font color="#A5A5A1">╰───────────────────────────────────────────────────╯</font>
<font color="#A5A5A1">╭─ Commands ────────────────────────────────────────╮</font>
<font color="#A5A5A1">│ </font><font color="#A1EFE4"><b>goodbye                                     </b></font>      │
<font color="#A5A5A1">│ </font><font color="#A1EFE4"><b>hello                                       </b></font>      │
<font color="#A5A5A1">╰───────────────────────────────────────────────────╯</font>

// You have 2 subcommands (the 2 functions): goodbye and hello
```

</div>

Now check the help for the `hello` command:

<div class="termy">

```console
$ python main.py hello --help

<b> </b><font color="#F4BF75"><b>Usage: </b></font><b>main.py hello [OPTIONS] NAME                 </b>
<b>                                                     </b>
<font color="#A5A5A1">╭─ Arguments ───────────────────────────────────────╮</font>
<font color="#A5A5A1">│ </font><font color="#F92672">*</font>    name      <font color="#F4BF75"><b>TEXT</b></font>  [default: None] <font color="#A6194C">[required]</font>   │
<font color="#A5A5A1">╰───────────────────────────────────────────────────╯</font>
<font color="#A5A5A1">╭─ Options ─────────────────────────────────────────╮</font>
<font color="#A5A5A1">│ </font><font color="#A1EFE4"><b>--help</b></font>          Show this message and exit.       │
<font color="#A5A5A1">╰───────────────────────────────────────────────────╯</font>
```

</div>

And now check the help for the `goodbye` command:

<div class="termy">

```console
$ python main.py goodbye --help

<b> </b><font color="#F4BF75"><b>Usage: </b></font><b>main.py goodbye [OPTIONS] NAME               </b>
<b>                                                     </b>
<font color="#A5A5A1">╭─ Arguments ───────────────────────────────────────╮</font>
<font color="#A5A5A1">│ </font><font color="#F92672">*</font>    name      <font color="#F4BF75"><b>TEXT</b></font>  [default: None] <font color="#A6194C">[required]</font>   │
<font color="#A5A5A1">╰───────────────────────────────────────────────────╯</font>
<font color="#A5A5A1">╭─ Options ─────────────────────────────────────────╮</font>
<font color="#A5A5A1">│ </font><font color="#A1EFE4"><b>--formal</b></font>    <font color="#AE81FF"><b>--no-formal</b></font>      [default: no-formal] │
<font color="#A5A5A1">│ </font><font color="#A1EFE4"><b>--help</b></font>                       Show this message    │
<font color="#A5A5A1">│                              and exit.            │</font>
<font color="#A5A5A1">╰───────────────────────────────────────────────────╯</font>

// Automatic --formal and --no-formal for the bool option 🎉
```

</div>

Now you can try out the new command line application:

<div class="termy">

```console
// Use it with the hello command

$ python main.py hello Camila

Hello Camila

// And with the goodbye command

$ python main.py goodbye Camila

Bye Camila!

// And with --formal

$ python main.py goodbye --formal Camila

Goodbye Ms. Camila. Have a good day.
```

</div>

### Recap

In summary, you declare **once** the types of parameters (*CLI arguments* and *CLI options*) as function parameters.

You do that with standard modern Python types.

You don't have to learn a new syntax, the methods or classes of a specific library, etc.

Just standard **Python 3.6+**.

For example, for an `int`:

```Python
total: int
```

or for a `bool` flag:

```Python
force: bool
```

And similarly for **files**, **paths**, **enums** (choices), etc. And there are tools to create **groups of subcommands**, add metadata, extra **validation**, etc.

**You get**: great editor support, including **completion** and **type checks** everywhere.

**Your users get**: automatic **`--help`**, **auto-completion** in their terminal (Bash, Zsh, Fish, PowerShell) when they install your package or when using <a href="https://typer.tiangolo.com/typer-cli/" class="internal-link" target="_blank">Typer CLI</a>.

For a more complete example including more features, see the <a href="https://typer.tiangolo.com/tutorial/">Tutorial - User Guide</a>.

## Optional Dependencies

Typer uses <a href="https://click.palletsprojects.com/" class="external-link" target="_blank">Click</a> internally. That's the only dependency.

But you can also install extras:

* <a href="https://rich.readthedocs.io/en/stable/index.html" class="external-link" target="_blank"><code>rich</code></a>: and Typer will show nicely formatted errors automatically.
* <a href="https://github.com/sarugaku/shellingham" class="external-link" target="_blank"><code>shellingham</code></a>: and Typer will automatically detect the current shell when installing completion.
    * With `shellingham` you can just use `--install-completion`.
    * Without `shellingham`, you have to pass the name of the shell to install completion for, e.g. `--install-completion bash`.

You can install `typer` with `rich` and `shellingham` with `pip install typer[all]`.

## License

This project is licensed under the terms of the MIT license.
