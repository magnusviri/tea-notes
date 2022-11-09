## Installing Tea

Installing is very easy. Here are the different ways you can install it.

Install Tea to ~/.tea

	sh <(curl https://tea.xyz)

Install Tea quietly.

	sh <(curl https://tea.xyz) -s

or

	YES=1 sh <(curl https://tea.xyz)

Specify the location of Tea.

	TEA_PREFIX=/opt/tea sh <(curl https://tea.xyz)

## Tea usage

Tea is not like other package managers. 

Basic idea.

	tea +pkg command args

Execute wget:

	tea +gnu.org/wget wget http://example.com

Run some Python

	echo 'print("hi")' | tea +python.org python

Run a Python script. The file "script.py":

	#!/usr/bin/env python
	
	print("Hi")

Run it:

	tea +python.org ./script.py


## History of Computing

This is a very quick introduction to the computer history that directly led to Tea.

### Libraries

To understand why Tea is significant, it helps to understand how we got here. When computers first started, developers wrote code and shared it with each other. They called the shared code libraries. When someone else used a shared library, they would call the library a dependency, because their project couldn't run without that library. There have always been 2 issues, installing and version control.

At first, there were only a few people who coded and work moved slowly. Installing and version control were not very good, except the developers were more skilled, so it wasn't as big of an issue. As more and more people became developers and as the pace of software development moved faster and faster, installing and version control became bigger and bigger problems.

One very good example of this was called "[DLL Hell](https://en.wikipedia.org/wiki/DLL_Hell)" on Windows computers during the 1990's. In general, this is called "[Dependency Hell](https://en.wikipedia.org/wiki/Dependency_hell)". There have been many solutions to this problem for end users, but developers still struggle with this problem.

One solution for developers is virtualizing the kernel and installing  different library versions in containers (Docker). Another is virtual environments and version locking. An example of this is [npm](https://en.wikipedia.org/wiki/Npm_(software)).

Tea offers a solution to this problem by using virtual environments.

### Open Source

In 1998, the U.S. Department of Justice and the Attorneys General of twenty U.S. states (and the District of Columbia) [sued Microsoft](https://en.wikipedia.org/wiki/United_States_v._Microsoft_Corp.) for illegally thwarting competition in order to protect and extend its software monopoly. There were so many examples of Microsoft breaking the law, that the prosecutors actually were overwhelmed with the scope. They knew that the best way to win was to limit the scope to the most obvious illegal behaviors. Microsoft's attacks on Netscape Navigator was one of the main examples in the case. Microsoft lost the case but some may feel the punishment was a hand slap.

However, before the trial began, Netscape was already struggling to survive. In an effort to survive and combat Microsoft, Netscape went [Open Source](https://en.wikipedia.org/wiki/Open_source). They didn't just become Open Source, they coined the term.

The [GNU](https://en.wikipedia.org/wiki/GNU) project existed before Netscape but they called what they were doing the "[free software movement](https://en.wikipedia.org/wiki/Free_software_movement)" ("free as in freedom, not free as in beer"). Some people did not some of things associated with GNU and "free software". The most relevant example is that because it had "free" in it's name no business would take a serious look at it.

So at the same time that Netscape went Open Source, the term, "Open Source" was created, which was a business friendly term. But the desire to make Open Source profitable extended far beyond it's name. They were successful because now we have Open Source companies like Red Hat, Canonical, and Hashicorp and we have Open Source products like Apache, MySQL, WordPress, and Elasticsearch. GitHub and GitLab are also Open Source havens.

### Nebraska Man

However, there are still a few problems. One problem is jokingly called the "[Nebraska Man](https://tea.xyz/nebraska-man/)" problem (not [this Nebraska Man](https://en.wikipedia.org/wiki/Nebraska_Man)). It comes from an XKCD comic titled "[Dependency](https://xkcd.com/2347/)". It refers to the day that Azer Koçulu unpublished his npm project named "[Left-pad](https://medium.com/lessons-from-history/the-man-who-broke-the-internet-by-deleting-11-lines-of-code-15b8f6f6f4c2)". Many websites failed because of it, including Netflix, Facebook, and Spotify.

As far as I know, nobody has tried to solve this problem.

Tea will solve this problem by immutably publishing packages on the [IPFS](https://en.wikipedia.org/wiki/InterPlanetary_File_System). This mechanism is still not set up.

### Unfunded or abandoned projects

Although OpenSource did make it possible to commercialize Open Source software, it only did so for companies with businessmen. A huge part of the Open Source community are individuals who write code in their free time and have no way to receive monetary compensation. Because of this, it is hard to keep the projects updated and secure. Many Open Source projects are completely abandoned, including some written by the author of this paragraph!

The best example of an unfunded project that was critical to many organizations is Log4J. At the end of 2021, [one of the most serious security vulnerabilities ever](https://en.wikipedia.org/wiki/Log4Shell) was discovered in Log4J. The Log4J developers fixed the bug, but the developers received a lot of [hate](https://www.franzoni.eu/log4j-haters-please/).

One solution to this problem is donations. For example, [GitHub Sponsors](https://github.com/sponsors) attempts make it possible to fund Open Source projects. However, these types of sponsorships only goes to one project or developer, not to the dependencies.

Tea will solve this with a Blockchain graph and NFTs. This feature should be released in 2023, and not much is known about it at this time.