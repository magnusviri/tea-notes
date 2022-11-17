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

## History of Computing

This is a very quick introduction to the computer history that directly led to Tea.

### Libraries

To understand why Tea is significant, it helps to understand how we got here. When computers first started, developers wrote code and shared it with each other. They called the shared code libraries. When someone else used a shared library, they would call the library a dependency, because their project couldn't run without that library. There have always been 2 issues, installing and version control.

At first, there were only a few people who coded and work moved slowly. Installing and version control was hard, except the developers were more skilled, so it wasn't as big of an issue. As more and more people became developers and as the pace of software development moved faster and faster, installing and version control became bigger and bigger problems.

In general, this is called "[Dependency Hell](https://en.wikipedia.org/wiki/Dependency_hell)". One very good example of this  on Windows computers in the 1990's was called "[DLL Hell](https://en.wikipedia.org/wiki/DLL_Hell)". There have been many solutions to this problem for end users, but developers still struggle with this problem.

One solution for developers is virtualizing the kernel and installing  different library versions in containers (Docker). Another is virtual environments and version locking. An example of this is [npm](https://en.wikipedia.org/wiki/Npm_(software)).

Tea offers a solution to this problem by using virtual environments.

### Open Source

In 1998, the U.S. Department of Justice and the Attorneys General of twenty U.S. states (and the District of Columbia) [sued Microsoft](https://en.wikipedia.org/wiki/United_States_v._Microsoft_Corp.) for illegally thwarting competition in order to protect and extend its software monopoly. There were so many examples of Microsoft breaking the law that the prosecutors actually were overwhelmed with the scope. They knew that the best way to win was to limit the scope to the most obvious illegal behaviors. Microsoft's attacks on Netscape Navigator was one of the main examples in the case. Microsoft lost the case but the punishment was a hand slap.

However, before the trial began, Netscape was already struggling to survive. In an effort to survive and combat Microsoft, Netscape went [open source](https://en.wikipedia.org/wiki/Open_source). They didn't just go open source, they coined the term. The [GNU](https://en.wikipedia.org/wiki/GNU) project existed before Netscape but they called what they were doing the "[free software movement](https://en.wikipedia.org/wiki/Free_software_movement)" ("free as in freedom, not free as in beer"). Some people did not like some of the things associated with GNU and "free software". The most relevant example is that because it had the word "free" in it's name, businesses would not take a serious look at it. So at the same time that Netscape went open source, they popularized the term "open source", which was business friendly. Linux also adopted the term.

The desire to make open source profitable extended far beyond it's name. The open source movement and the desire to make open source commercially viable was successful. Now we have open source companies like Red Hat, Canonical, and Hashicorp. We have open source products like Apache, MySQL, WordPress, and Elasticsearch. The internet runs on Linux. GitHub and GitLab are open source havens. Microsoft even purchased GitHub and has some open source projects of their own (including Visual Studio Code).

#### Nebraska Man

However, there are still a few problems. One problem is jokingly called the "[Nebraska Man](https://tea.xyz/nebraska-man/)" problem (not [this Nebraska Man](https://en.wikipedia.org/wiki/Nebraska_Man)). It comes from an XKCD comic titled "[Dependency](https://xkcd.com/2347/)". It refers to the day that Azer Koçulu unpublished his npm project named "[Left-pad](https://medium.com/lessons-from-history/the-man-who-broke-the-internet-by-deleting-11-lines-of-code-15b8f6f6f4c2)". Many websites failed because of it, including Netflix, Facebook, and Spotify.

As far as I know, nobody has tried to solve this problem.

Tea will solve this problem by immutably publishing packages on the [IPFS](https://en.wikipedia.org/wiki/InterPlanetary_File_System). This mechanism is still not set up.

#### Unfunded or abandoned projects

Although open source did make it possible to commercialize open source software, it only did so for companies with businessmen. A huge part of the open source community are individuals who write code in their free time. No matter how generous people are, everyone has to eat and that requires money. Lack of funding has led to many abandoned open source projects, including some written by the author of this paragraph! And lack of funds makes it hard for generous developers to give projects the time they deserve.

The best example of an unfunded project that was critical to many organizations is Log4J. At the end of 2021, [one of the most serious security vulnerabilities ever](https://en.wikipedia.org/wiki/Log4Shell) was discovered in Log4J. The Log4J developers fixed the bug, but the developers received a lot of [hate](https://www.franzoni.eu/log4j-haters-please/).

One solution to this problem is donations. For example, [GitHub Sponsors](https://github.com/sponsors) attempts to make it possible to fund open source projects. However, these types of sponsorships only go to one project or developer, not to the dependencies.

Tea will solve this with a Blockchain graph and NFTs. This feature should be released in 2023, and not much is known about it at this time.
