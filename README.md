# tea-test

Testing Tea.xyz

Test this yourself by running `sh <(curl tea.xyz) https://github.com/magnusviri/tea-test/blob/main/README.md`

    echo "test 1"

# Getting Started

    echo "test 2"

## Getting Started

    echo "test 3"

## Something else

    echo "test 4"

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
