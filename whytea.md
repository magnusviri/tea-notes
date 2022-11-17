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
