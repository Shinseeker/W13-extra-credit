#####################
Marshal:Serialization
#####################

By Jake Kwok

.. Image:: https://upload.wikimedia.org/wikipedia/en/6/69/Marshall_logo.svg

About Importing Marshal
=======================
This module is in the python library and contains functions that can read 
and write Python values in a binary format. The format is specific to Python, 
but independent of machine architecture issues 
(e.g., you can write a Python value to a file on a PC.)

However, it does not store as many objects as pickle because the module exists mainly 
to support reading and writing the “pseudo-compiled” code for Python modules of .pyc files. 
Therefore, the Python maintainers reserve the right to modify the marshal format 
in backward incompatible ways should the need arise.


Marshal's Functions
===================
There are functions that read/write files as well as functions operating on strings.

1.marshal.dump(value, file[, version])

Write the value on the open file. The value must be a supported type. The file must be a 
open file object such as sys.stdout or returned by open() or os.popen(). 
It may not be a wrapper such as TemporaryFile on Windows. 

2.marshal.load(file)

Read one value from the open file and return it. If no valid value is read 
(e.g. because the data has a different Python version’s incompatible marshal format), 
raise EOFError, ValueError or TypeError. The file must be an open file 
object opened in binary mode ('rb' or 'r+b').


Marshal is Fast
===============


Although Marshal is limited in how many characters you can use. It 
remains one of the Fastest Serlization tools in the python library.

1cjson
-time_serializer took 416.574 ms

2.simplejson
-time_serializer took 544.954 ms

3.jsonlib
-time_serializer took 470.916 ms

4.jsonlib2
-time_serializer took 502.131 ms

5.pickle
-time_serializer took 9550.609 ms

6.cPickle
-time_serializer took 672.311 ms

7.marshal
-time_serializer took 167.835 ms

Marshal comes out the fastest... but what you get in speed, you pay for in readability, 
portability and safety. (See the note on the webpage for Marshal and pickle
on deserializing malicious strings.)

If you want more details go to this site. They provide a code that you can take a
look at:
- http://www.lorieau.com/methods-and-reference/computers-and-programming/21-python-serializers

My Thoughts
============

To a degree Marshal is good if you want to serilize the basic python fundamentals like
You have a Python data structure composed of only fundamental Python objects 
e.g., lists, tuples, numbers, and strings, but no classes, instances, etc.
and you want to serialize it and reconstruct it later as fast as possible.
Otherwise i would use pickle because you can pretty much serialize all the concepts.

Refrences
=========

- https://docs.python.org/2/library/marshal.html

- http://www.lorieau.com/methods-and-reference/computers-and-programming/21-python-serializers
