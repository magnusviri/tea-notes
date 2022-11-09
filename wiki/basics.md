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

To understand why Tea is significant, it helps to understand how we got here. When computers first started, there were few people working on them and work moved slowly. Because of that, building, installing, and updating stuff was slow. If you installed software, it was reasonable that it would stay installed 
