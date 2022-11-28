## tea-notes

My tea.xyz notes (I should have this on my website but it's here for now).

Tea works in the terminal. If you don't know how to use the terminal, please do a web search for "unix terminal" and read a little bit before trying anything here.

You should probably read the [CLI readme](https://github.com/teaxyz/cli) first.

## Installing Tea

If you are on Windows, you first need to install [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/about) (WSL).

In the macOS or Linux terminal (Windows users need to use the WSL terminal), just type this command in.

```
sh <(curl https://tea.xyz)
```

The installer will ask if you want to create a symlink in /usr/local/bin. I would select yes. It will also ask if it can modify ~/.zshrc. Basides those 2 changes, tea doesn't change anything outside of it's directory.

Tea will be installed to ~/.tea.

The tea installer is located at https://tea.xyz (when loaded by curl, it returns the installer instead of the webpage). 


Here are some of the options when you install tea. For example, you can install it silently (answering yes to all the questions).

	sh <(curl https://tea.xyz) -s

or

	YES=1 sh <(curl https://tea.xyz)

You can specify the location of Tea.

	TEA_PREFIX=/opt/tea sh <(curl https://tea.xyz)

To update tea, just run the same installer.

	sh <(curl https://tea.xyz)

## Basic Tea Usage

Tea is not like other package managers. It's more like an environment manager.

In it's most basic form, Tea will install a package if needed and run a command or open a REPL with the package in the PATH.

	tea +pkg

To avoid the REPL, specify a command (and optional args).

	tea +pkg command [args]

Example, execute wget.

	tea +gnu.org/wget wget http://example.com

Example, run some Python.

	echo 'print("hi")' | tea +python.org python

Example, run a Python script. Here is a file named "script.py".

```
#!/usr/bin/env python

print("Hi")
```

Run it like this.

	tea +python.org ./script.py

If a file ends in ".py", tea will automatically add +python.org. It helps to understand what is going on behind the scenes though, which is why I explained everything. Run it like this.

	tea ./script.py

## Use Tea to Install Something

Right now there is no difference between running something with Tea and installing something and running it. So if you only want to install something, then run a command that doesn't do anything.

Example, install Python if missing.

	tea +python.org python --version

Or 

	tea +python.org echo ""

There's a lot more information on installing stuff on the [replacing brew](https://github.com/magnusviri/tea-notes/blob/main/replacing-brew.md) page.

## Intermediate Tea usage

You can specify multiple packages and create a REPL with those dependencies in the PATH.

	tea +invisible-island.net/ncurses +sourceware.org/bzip2 +tea.xyz/gx/cc +gnu.org/make

Specify a specific version of a package.

	tea +python.org=3.10.8 python

Specify a minimum version. This will run the latest python 3.10.x.

	tea +python.org^3.10.0 python

This will run the latest python 3.x.

	tea +python.org^3.10 python

## Tea PATH

Note, tea doesn't add anything it installs to the PATH. That means you must use tea to run stuff installed by tea. If you would like the stuff you install added to the path then you can do a few things. Starting with the cli v0.14.5, you can create a symlink to tea using the name of the tool you'd like.

```
sudo ln -s tea /usr/local/bin/wget
```

That will create a symnlink for wget. And it just works!

## Executable markdown

Running `sh <(curl tea.xyz) https://github.com/magnusviri/tea-notes/blob/main/README.md` will search this document and do the following.

- Searches for `/^#+\s+${arg[0].replaceAll(/ /, "-")}\s*$/i`
- Executes a block delineated by `/^```sh\s*$/ and /^```\s*$/`

It will execute this:

### Getting Started

```
echo "test 1"
```

#### Getting Started

```
echo "test 2"
```

### Test3

Adding an argument `sh <(curl tea.xyz) https://github.com/magnusviri/tea-notes/blob/main/README.md Test3` will search this document for the argument and execute the code block.

```
echo "test 3"
```
