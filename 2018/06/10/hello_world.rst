=============================
iter function with sentinnel 
=============================

.. author:: Smital Desai
.. categories:: trick
.. tags:: iter


Hello Pythonistas, did you know that Python iter function has a two arg variant ?

.. code-block:: python

	iter(func, sentinnel)

However the func - must be a zero argument callable.

.. code-block:: python

       for _ in iter(func, sentinnel):
           do_something()  

In this case, loop will run only till func produces the sentinnel value.

**Some use cases :** 
     1. Run a game loop for specific duration 
     2. Read lines from file  till particular match is found 
     3. Read data from socket in chunk sizes 

---------------
First Example :
---------------

.. code-block:: python

	In [14]: from functools import partial
	
	In [15]: import random
	
	In [16]: genrate_nums = partial(random.randint, 1, 10) # Generate random numbers between 1, 10
	
	In [17]: genrate_nums() # a random number between 1 and 10 is returned.
	Out[17]: 5
	
	In [18]: genrate_nums()
	Out[18]: 2

Lets look at these two runs. The varying number of iterations in two cases indicate that in the first run the sentinnel 
was returned from our `generate_nums` function when it was called 5th time and in the next run the setinnel value was returned when 
the `generate_nums` was called for 14th time.

.. code-block:: python

	In [23]: for i in iter(genrate_nums, 5):
	    ...:     print(i)
	    ...:

	1
	2
	9
	4

	In [24]: for i in iter(genrate_nums, 5):
	    ...:     print(i)
	    ...:

	4
	10
	9
	3
	2
	8
	1
	9
	3
	7
	8
	3
	2
	1

----------------
Second Example :
----------------	

Lets look at another example where we have a file called 'hello.txt'
We wish to read lines in file will the line contains "hello"
So effectively we wish to read only first two lines in this files.

Lets see how we can go about achieving the same.

.. code-block:: python

	In [14]: cat 'hello.txt'
	sdfasd
	sdfdfdf
	hello
	sdfasd
	asdfasd
	
	In [15]: with open('hello.txt') as file:
	    ...:     for line in iter(file.readline, "hello\n"):
	    ...:         print(line, end='')
	    ...:
	    ...:
	sdfasd
	sdfdfdf
