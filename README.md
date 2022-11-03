# tea-notes

My Tea.xyz notes (I should have this on my website but it's here for now).

## Notes from  2022-11-03 AMA.

Tea CLI is written in TypeScript and compiled to binary using deno (https://deno.land/).

Tea installs to ~/.tea, sandboxed. It sandboxes throughout. It was written as virtual environment manager first. That way you can have multiple versions of the same software installed. This can be changed with env vars. Everything is compiled to be relocatable (this wasn't easy). They are activating virtual environments by using zsh directory hooks.

Tea doesn't need to be installed. If you run it from the web (`sh <(curl tea.xyz) ...`), it will create an environment in /tmp (which is usually deleted periodically, I think on macOS it is cleaned out when you reboot). `sh <(curl tea.xyz)` (no arguments) will install the `tea` cli. If you have `tea` installed, you can replace all instances of `sh <(curl tea.xyz)` with `tea` (and vise-versa).

On macOS, Xcode Command Line Tools isn't required if the package doesn't need to be compiled to install or run it. If the package needs to be compiled, Tea comes with a compiler but it works better with Apple's and it will prompt you to use it.

Tea can "execute" markdown. If a markdown file includes a "# Getting Started" section (I'm not sure if it's "#" or "##" yet), then `sh <(curl tea.xyz) https://github.com/my/project` will execute the code in that section. I actually couldn't get this to work yet.

Private pantries are possible. Tea has their own internal QA server for testing out stuff before they deploy it.

Remuneration: Tea tokens isn't all about earning money. Remuneration can also be passed 100% to it's dependencies or donated to charity.

I think "universal interpretation" means that it can install whatever interpreter is required for a script. So `tea +python.org ./test.py` will install python if it's missing, then it will launch test.py and pass it to python. Here's some examples of running python code. The following will print "Hi" using Python.

	echo 'print("hi") | tea +python.org python

To exexute a python script, do the following.

	tea +python.org ./script.py

And this is the script:

	#!/usr/bin/env python
	
	print("Hi")

I think `+python.org` will install python or add python to the path.

At this stage, Tea isn't a replacement for Homebrew. The biggest reason is that using Tea looks like this.

	tea +identifier command args

This is how you execute wget:

	tea +gnu.org/wget wget http://example.com

Tea will not create an alias or add wget to the PATH variable. That's because Tea is so heavily wrapped up in virtual environments and right now Tea is targeting developers. But you can do add aliases yourself.

	alias wget="tea +gnu.org/wget wget"

Or even better, if you're using zsh, you can put this in your .zshrc or something (I don't know how it handles spaces yet).

	function command_not_found_handler {
		found=`(ls ~/.tea/*/*/v\*/bin/"$1") 2>/dev/null`
		if [[ -x $found ]]; then
			set -- "${@:2}"
			$found $@
		else
			echo "Command Not Found: $1"
		fi
	}

Or you can even do this.

	echo "#!/bin/sh\ntea +gnu.org/wget wget $*" >/usr/local/bin/wget

I don't think you can add Tea's paths to the PATH variable because there isn't one path. Each item is split into it's domain and versions and it looks like they each have their own bin directory. Again, this is how virtual environments work.

I believe for developers, the different virtual environments are activated with zsh directory hooks. I don't know how that works yet.

## Notes from  2022-10-14 webcast.

There’s 2 types of package managers. At the OS level you have apt, yum, brew, etc. These download or produce binaries. Then there are software dependency managers like npm, pip, Cargo, gems, etc. These download source code.

Tea is more of an OS level package manager at this point but it aims to be both. It is attempting to simplify and unify all of these things. They are hoping to create a paradigm. Their goal is to abstract the package manager away, to create a unified package manager.

No one has tried to make a funded package manager. There are a lot of package managers that started as small projects but grew so big that they needed funding. Nobody has tried to integrate package managers and so there is a lot of duplicated work in this space.

They are building Tea primitives and they hope that they will become the foundation used by all kinds of tools and facilitate integrations across them. They don’t intend on “Sherlocking” software package managers like npm. They’re hoping that the dependency managers will adopt the Tea primitives.

They are creating a Tea protocol that other package managers can use. The Tea protocol will be governed from Switzerland. [Zug, located 20 miles south of Zurich, is known as Crypto valley. There are about 750 Crypto companies located there. It’s the only government that accepts Bitcoin and they’ve given all of their residents crypto ID’s. Local businesses are also switching over to Bitcoin. This pattern is spreading to other parts of Switzerland like Geneva. The Swiss government is trying to become the “Blockchain Nation”.] Tea is going to use the security and renumeration features of crypto. Users don’t need to know that aspect exists.

Tea is expected to launch this year (November?). Tea will deploy binaries and work on Mac and Linux, x86 and Arm (which they call AR 64). The Linux binaries will work with any Linux. They are using glibc version 23 (which is old and API stable) to compile the Linux binaries. They will support Windows as soon as possible. They also plan on supporting OS’es other than Mac, Windows, and Linux. They don’t want the OS to matter.

Tea should have decentralized package registry support by launch. The decentralized blockchain package registry should be working next year. In the long term the goal is to have everything decentralized. They will also support having multiple package registries [I believe this includes private registries].

Tea will have sub commands and be scriptable like npm and cargo. They want it make it so that you can install stuff from a webpage link, the command line, or in scripts.

A developer lists dependencies in a recipe and Tea brings them into the environment when needed. The dependencies wont pollute your environment when you don’t need them. The Tea “database” is going to be the filesystem and it will use symlinks. You will be able to mix and match versions like npm where requirements are pinned.

Package recipes will be stored in “pantries”. People will be able to host their own pantries. Tea will be able to find pantries and people won’t have to add them manually. There is a lot they can’t legally say about this until they launch.

Tea is still pre-release, but you can try it out (I suggest doing it in a Docker container or something that can be thrown away).

	sh <(curl tea.xyz) +charm.sh/gum gum spin -- sleep 5

If you run that command it downloads files to /tmp and runs from there. Pretty nifty.

This will install tea: `sh <(curl tea.xyz)`

## Testing executable markdown.

Test this by running `sh <(curl tea.xyz) https://github.com/magnusviri/tea-notes/blob/main/README.md`. It's currently not working or I'm doing something wrong.

# Getting Started

    echo "test 2"

## Getting Started

    echo "test 3"

## Something else

    echo "test 4"
