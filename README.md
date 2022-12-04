# tea-notes

I've moved most of these notes to the [tea wiki](https://github.com/teaxyz/cli/wiki/Basics).

Here's what I haven't moved.

---


## Advanced Usage

You can specify multiple packages and create a REPL with those dependencies in the PATH.

	tea +invisible-island.net/ncurses +sourceware.org/bzip2 +tea.xyz/gx/cc +gnu.org/make



Everything is compiled to be relocatable (this wasn't easy)

They are activating virtual environments by using zsh directory hooks.

## Executable markdown

I don't believe this works yet!

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

