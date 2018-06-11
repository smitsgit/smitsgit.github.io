============================================
Understanding decorator pattern with Python
============================================

.. author:: Smital Desai
.. categories:: programming
.. tags:: pattern

.. image:: hazelnut-cream-hot-chocolate.jpg

Hello Pythonistas, Lets implement decorator pattern in Python.
I am a big fan of Head first design patterns book so lets take an example from that book.

When we go to coffee shop like Starbucks or Barista , sometimes
we also like to add toppings to the coffee of our liking, like **whipped cream / ice cream / nutella.**

""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
What we are essentially doing is we are decorating our coffee with these extra toppings or condiments.
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Now imagine you are the owner of the coffee shop and you wish to determine the price of such item thats decorated
with condiments.

Its safe to say that there is base price associated with coffee and so is with each condiments

1. Coffee - price 50 [ Base price ]
2. Whipped Cream - 10 
3. Nutella - 30 

1. If you opt for **coffee with whipped cream** - Price will be 60  [ Base price + 10]
2. If you opt for **coffee with Nutella** - Price will be 80  [ Base price + 30 ]
3. If you opt for **coffee with Nutella and whipped cream** - Price will be 90 [ Base price + 30 + 10]


.. code-block:: python

	In [82]: from functools import wraps
	
	In [83]: def whipped_cream(func):
	    ...:     @wraps(func)
	    ...:     def wrapper(*args, **kwargs):
	    ...:         price = func(*args, **kwargs)
	    ...:         price = price + 10
	    ...:         return price
	    ...:     return wrapper
	    ...:
	    ...:
	
	In [84]: def nutella(func):
	    ...:     @wraps(func)
	    ...:     def wrapper(*args, **kwargs):
	    ...:         price = func(*args, **kwargs)
	    ...:         price = price + 30
	    ...:         return price
	    ...:     return wrapper
	    ...:
	    ...:
	
	In [85]: def coffee():
	    ...:     return 50
	    ...:
	    ...:
	
	In [86]: @whipped_cream
	    ...: def coffee_with_whipped_cream():
	    ...:     return coffee()
	    ...:
	    ...:
	
	In [87]: coffee_with_whipped_cream()
	Out[87]: 60
	
	In [88]: @whipped_cream
	    ...: @nutella
	    ...: def coffee_with_nutella_and_whipped_cream():
	    ...:     return coffee()
	    ...:
	    ...:
	
	In [89]: coffee_with_nutella_and_whipped_cream()
	Out[89]: 90 
	