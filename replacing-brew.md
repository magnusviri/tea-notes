# Switching from brew with tea

Install tea if you haven't already.

    sh <(curl https://tea.xyz)

## Get the brew list

Get your list of items installed with brew.

    brew list

Most of the things in my list are libraries installed with other tools like ca-certificates, gnutls, libogg, libpng, etc. Find the things that you want.

## See what tea's got

You can see what tea has available on [tea.xyz](https://tea.xyz).

You can also list the packages by searching the pantry. This command will just print the items available.

    find ~/.tea/tea.xyz/var/pantry/projects -name package.yml | sed -e 's/.*\/projects\/\(.*\)\/package.yml/\1/'

However, packages can contain many tools. For example, if you install perl, it has [30 items](https://github.com/teaxyz/pantry.core/blob/main/projects/perl.org/package.yml) in it's bin directory. You can view the full list by finding the "provides" section in the package.yml file (e.g. `cat /opt/tea.xyz/var/pantry/projects/perl.org/package.yml`). I'm sure in time there will be an easier way to do this. You can also search for "- bin/" in all of the package.yml files.

    find ~/.tea/tea.xyz/var/pantry/projects -name package.yml -exec grep -- "- bin/" \{\} \;

## Uninstall the brew version

Replace *name* with what you want uninstalled.

    brew uninstall *name*

## Install the tea version

Replace "pkg" with the package you want. If it installed correctly, `which *name*` should list the tea version

    tea +pkg which -a *name*

## Example

I've installed curl with tea. `which -a curl` will display all of the curls in the PATH.

    > tea which -a curl
    /usr/bin/curl
    > tea +curl.se which -a curl
    /opt/tea/curl.se/v7.86.0/bin/curl
    /usr/bin/curl

## Create symlink

By default tea wont symlink anything it installs to /usr/local/bin or modify the PATH. Here's some [ideas about how to handle that](https://github.com/magnusviri/tea-notes/blob/main/README.md#tea-path)..
