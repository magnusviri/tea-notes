## tea-notes

My Tea.xyz notes (I should have this on my website but it's here for now).

You should probably read the [CLI readme](https://github.com/teaxyz/cli) first.

## Installing Tea

Installing is very easy. Here are the different ways you can install it. Note, all the docs leave off the "https://", but you really should use it. To make it easier, all of my examples have it.

The tea installer is located at https://tea.xyz (when loaded by curl, it returns the installer instead of the webpage).

When you install tea using the installer, it will ask if you want to create a symlink in /usr/local/bin. It will also ask if it can modify ~/.zshrc. Basides those 2 changes, tea doesn't change anything outside of it's directory.

Install Tea to ~/.tea

	sh <(curl https://tea.xyz)

Install Tea quietly.

	sh <(curl https://tea.xyz) -s

or

	YES=1 sh <(curl https://tea.xyz)

Specify the location of Tea.

	TEA_PREFIX=/opt/tea sh <(curl https://tea.xyz)

Update tea. It's the same as installing.

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

## Intermediate Tea usage

You can specify multiple packages and create a REPL with those dependencies in the PATH.

	tea +invisible-island.net/ncurses +sourceware.org/bzip2 +tea.xyz/gx/cc +gnu.org/make

Specify a specific version of a package (note, check [issue 156](https://github.com/teaxyz/cli/issues/156) to see if this works yet).

	tea +python.org=3.10.8 python

Specify a minimum version. This will run the latest python 3.10.x.

	tea +python.org^3.10.0 python

This will run the latest python 3.x.

	tea +python.org^3.10 python

## Tea PATH

Note, tea doesn't add anything it installs to the PATH. That means you must use tea to run stuff installed by tea unless you do something yourself. You can't just add a single bin directory either. Each item is split into it's domain and versions and they each have their own bin directory.

Here's some ideas to solve this.

### Custom /usr/local/bin/tea

I'm leaning towards creating a custom /usr/local/bin/tea and linking all the tools I want to it. I'm not too sure this will scale well though.

Here is my [/usr/local/bin/tea](https://github.com/magnusviri/tea-notes/blob/main/usr/local/bin/tea)

Then for each of my commands I link them to tea.

	ln -s tea /usr/local/bin/jq

I tried `tea -X`, but if tea hasn't installed the package, then `tea` will actually execute the link at /usr/local/bin, which causes the script to run all over, so it gets into an endless loop. I'm sure over time a better solution will come up.

### Stub file

This is very similar to the above method. I like the above method more because there's only one file to edit, and it is easy to find all of the tea stuff, just find all the links to /usr/local/bin/tea.

	echo "#!/bin/sh\ntea +gnu.org/wget wget $*" >/usr/local/bin/wget

### Alias

Put this code in ~/.zshrc.

	alias wget="tea +gnu.org/wget wget"

### zsh command_not_found_handler

Put this in ~/.zshrc. I don't know how it handles spaces. The other problem with it is that `which` doesn't work with it.

	function command_not_found_handler {
		if [ -z "${TEA_PREFIX+1}" ]; then
			TEA_PREFIX=~/.tea
		fi
		found=`(ls $TEA_PREFIX/**/v\\*/bin/"$1") 2>/dev/null`
		if [[ -x $found ]]; then
			set -- "${@:2}"
			$found $@
		else
			echo "Command Not Found: $1"
		fi
	}

Tea now discusses this on [their page](https://github.com/teaxyz/cli#may-we-interest-you-in-a-hack). It's far simpler than what I've got though.

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
