.. _tut-morecontrol:

***********************
More Control Flow Tools
***********************

Өөрөөр хэлбэл :keyword:`while` илэрхийлэл бол Пайтон хэл болон
өөр хэлнүүдэд байдаг урсгал удирдах илэрхийлэл юм.



.. _tut-if:

:keyword:`if` илэрхийлэл
========================

Голчлон хэрэглэгддэг илэрхийллүүдийн нэг бол :keyword:`if` илэрхийлэл юм.  Жишээ::

   >>> x = int(raw_input("Бүхэл тоо оруул: "))
   Бүхэл тоо оруул: 42
   >>> if x < 0:
   ...      x = 0
   ...      print 'Сөрөг тоо тэгээр солигдлоо'
   ... elif x == 0:
   ...      print 'Тэг'
   ... elif x == 1:
   ...      print 'Нэг'
   ... else:
   ...      print 'Нэгээс их'
   ...
   More

Таны оруулсан тоо тэг болон нэг байгаа эсэхийг :keyword:`elif` түлхүүрээр,бусад тохиолдолд :keyword:`else` түлхүүрээр
шалгаж байна.':keyword:`elif`' түлхүүр үг бол 'else if' гэдгийг товчлон, илүү
бичихэд амархан болгосон. :keyword:`if` ... :keyword:`elif` ...
:keyword:`elif` ... түлхүүрийг урт дараалсан нөхцөл шалгахад зарим хэлэнд
``switch`` болон ``case``  илэрхийлэл байдаг.


.. _tut-for:

:keyword:`for` илэрхийлэл
=========================

.. index::
   statement: for
   statement: for

:keyword:`for` илэрхийлэл нь Пайтон хэлэнд бидний өмнө хэрэглэж заншсан С болон 
Паскал хэлний for илэрхийллээс бага зэрэг илүү гэж болно. Арифметик прогресийн
өсөх дугаараар гүйн давтах(Pascal шиг), эсвэл эхлэх болон төгсгөл, алхамыг 
өгөн нөхцлөөр зогсон давтаж( C шиг ), Пайтонгийн :keyword:`for` илэрхийлэл нь
ямар нэг давтамжийн элементээр гүйж  (жагсаалт эсвэл тэмдэгт), давтамжийг
харуулна. Жишээлбэл :


::

   >>> # Зарим тэмдэгтийг хэмжих:
   ... a = ['cat', 'window', 'defenestrate']
   >>> for x in a:
   ...     print x, len(x)
   ...
   cat 3
   window 6
   defenestrate 12

Жагсаалтаар гүйхэд юу ч өөрчлөхгүй (энэ нь зөвхөн хувирамтгай жагсаалт ,дараалалд тохиолдоно).  Хэрвээ жагсаалтаар гүйнгээ өөрчлөх бол гүйхдээ хуулах 
хэрэгтэй (жишээлбэл сонгогдсон элементийг хуулбарла).Ингэж хувааснаар илүү 
амар болдог.::

   >>> for x in a[:]: # make a slice copy of the entire list
   ...    if len(x) > 6: a.insert(0, x)
   ...
   >>> a
   ['defenestrate', 'cat', 'window', 'defenestrate']


.. _tut-range:

The :func:`range` функц
=======================

Хэрэв та тоо өгөн түүгээр дараал үүсгэх бол :func:`range` өгөгдсөн тоогоор 
дараалал үүсгэнэ.  Дараалал үүсгэхдээ арифметик прогрессоор үүсгэнэ::

   >>> range(10)
   [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

Дараалал үүсгэхдээ төгсгөлийн цэгийг өгнө; ``range(10)`` нь 10 утгатай жагсаалт
үүсгэн, 10 урттай индеклэсэн дараалал болгов. Мөн дараалал ямар тооноос эхлэх 
болон ямар утгаар өсөхийг ч зааж өгч болно.(эерэг тоо байх ба заримдаа алхам ч гэж нэрлэдэг)::

   >>> range(5, 10)
   [5, 6, 7, 8, 9]
   >>> range(0, 10, 3)
   [0, 3, 6, 9]
   >>> range(-10, -100, -30)
   [-10, -40, -70]

Дарааллын элементээр гүйн элементийг индеклэхдээ  :func:`range` болон 
:func:`len` функцийн хослолыг хэрэглэхийг дор үзүүлэв::

   >>> a = ['Mary', 'had', 'a', 'little', 'lamb']
   >>> for i in range(len(a)):
   ...     print i, a[i]
   ...
   0 Mary
   1 had
   2 a
   3 little
   4 lamb

Ихэнд тохиолдолд дээрхийг хэрэглэдэг ч :func:`enumerate` функцийг хэрэглэх нь
тохиромжтой. үз :ref:`tut-loopidioms`.

.. _tut-break:

:keyword:`break` ба :keyword:`continue` илэрхийллүүд, болон :keyword:`else` нөхцөл давталт дээр
===============================================================================================

:keyword:`break` илэрхийлэл нь яг С хэлэн байдаг шиг :keyword:`for` болон 
:keyword:`while` давталтанд дотор зогсоох үйлдлийг хийдэг.

:keyword:`continue` илэрхийлэл нь С хэлнээс удамшсан давталтыг дараагийх руу
шилжүүлж үргэлжлүүлдэг.

Давталт илэрхийлэл нь  ``else`` нөхцөлтэй байж болно; (:keyword:`for`-той хамт) эсвэл ( :keyword:`while` хамт) нөхцөл худал болвол давталтыг зогсооход ашиглана. , гэвч :keyword:`break` илэрхийлэлгүйгээр зогсохгүй.Давталтын жишээг анхны
тоог олох жижиг жишээн дээр үзүүлье.::

   >>> for n in range(2, 10):
   ...     for x in range(2, n):
   ...         if n % x == 0:
   ...             print n, 'equals', x, '*', n/x
   ...             break
   ...     else:
   ...         # loop fell through without finding a factor
   ...         print n, 'is a prime number'
   ...
   2 is a prime number
   3 is a prime number
   4 equals 2 * 2
   5 is a prime number
   6 equals 2 * 3
   7 is a prime number
   8 equals 2 * 4
   9 equals 3 * 3


.. _tut-pass:

:keyword:`pass` илэрхийлэл
==========================

The :keyword:`pass` илэрхийлэл нь юу ч хийхгүй. Тодорхой шаардлагаар ямар ч үйлдэл хийхгүй зөвхөн синтаксийн шаардлагаар юм бичих тохиолдолд хэрэглэж болно.Жишээлбэл::

   >>> while True:
   ...     pass  # Busy-wait for keyboard interrupt (Ctrl+C)
   ...

Үүнийг жижиг класс үүсгэхэд нийтлэг хэрэглэдэг::

   >>> class MyEmptyClass:
   ...     pass
   ...

:keyword:`pass` илэрхийллийг хэрэглэх өөр нэг хувилбар бол хийсвэр функц эсвэл
нөхцөлт бие-ийг шинээр бичин хийсвэрлэх түвшинд бичиж байгаа үед ашигладаг. 
Үүнд :keyword:`pass` бол шууд зөвшөөрөгдөнө.::

   >>> def initlog(*args):
   ...     pass   # Remember to implement this!
   ...

.. _tut-functions:

Функц зарлах
============

Бид Фибаночийн дараалал үүсгэх жишээг авч функц үүсгэе::

   >>> def fib(n):    # write Fibonacci series up to n
   ...     """Print a Fibonacci series up to n."""
   ...     a, b = 0, 1
   ...     while a < n:
   ...         print a,
   ...         a, b = b, a+b
   ...
   >>> # Now call the function we just defined:
   ... fib(2000)
   0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597

.. index::
   single: documentation strings
   single: docstrings
   single: strings, documentation

:keyword:`def` түлхүүр үгээр функцыг *тодорхойлолно*.  Үүний араас функцийн нэр
байх ба хаалтан дотор параметруудын жагсаалтыг бичиж өгч болно.
Энэ илэрхийллийн дараагийн мөрөөс эхлэн функцын бие байх бөгөөд мөрүүд нэг 
зэрэгцсэн байх ёстой.(must be indented).

Функцын биеийн эхний мөр нь тэмдэгт тайлбар байж болно;
энэ тэмдэгт нь функцын баримтжуулалтын тэмдэгт, эсвэл :dfn:`docstring` 
байж болно.
(docstrings-ийн тухай дэлгэрэнгүй мэдээллийг:ref:`tut-docstrings`-ээс үзэж болно.)
Зарим хэрэгслүүд docstring-ийг ашиглан онлайн болон хэвлэмэл баримтыг
автоматаар үүсгэдэг, эсвэл хэрэглэгч түүгээр эх кодын ажиллагааг мэднэ; 
docstring ашиглан код бичснээр өөртөө маш сайн дадлага туршлагатай болно. 

Функцын *ажиллагаа*  нь функц дотор локал хувьсагч үсэг ашиглан 
зарлаж эхэлсэн байна. Өөрөөр хэлбэл функцын бүх утга олголт өөрийн локаль 
тэмдэгтийн хүснэгтээс авч ашигласан байна; Глобаль хувьсагч функцээс шууд утга 
олгож болохгүй бөгөөд тусгай функц ашигладаг(:keyword:`global` илэрхийллээр).

The actual parameters (arguments) to a function call are introduced in the local
symbol table of the called function when it is called; thus, arguments are
passed using *call by value* (where the *value* is always an object *reference*,
not the value of the object). [#]_ When a function calls another function, a new
local symbol table is created for that call.

A function definition introduces the function name in the current symbol table.
The value of the function name has a type that is recognized by the interpreter
as a user-defined function.  This value can be assigned to another name which
can then also be used as a function.  This serves as a general renaming
mechanism::

   >>> fib
   <function fib at 10042ed0>
   >>> f = fib
   >>> f(100)
   0 1 1 2 3 5 8 13 21 34 55 89

Coming from other languages, you might object that ``fib`` is not a function but
a procedure since it doesn't return a value.  In fact, even functions without a
:keyword:`return` statement do return a value, albeit a rather boring one.  This
value is called ``None`` (it's a built-in name).  Writing the value ``None`` is
normally suppressed by the interpreter if it would be the only value written.
You can see it if you really want to using :keyword:`print`::

   >>> fib(0)
   >>> print fib(0)
   None

It is simple to write a function that returns a list of the numbers of the
Fibonacci series, instead of printing it::

   >>> def fib2(n): # return Fibonacci series up to n
   ...     """Return a list containing the Fibonacci series up to n."""
   ...     result = []
   ...     a, b = 0, 1
   ...     while a < n:
   ...         result.append(a)    # see below
   ...         a, b = b, a+b
   ...     return result
   ...
   >>> f100 = fib2(100)    # call it
   >>> f100                # write the result
   [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]

This example, as usual, demonstrates some new Python features:

* :keyword:`return` илэрхийлэл нь функцээс утга буцаадаг.
  :keyword:`return` илэрхийллээр ``None`` утга буцаана. Falling off
  the end of a function also returns ``None``.

* The statement ``result.append(a)`` calls a *method* of the list object
  ``result``.  A method is a function that 'belongs' to an object and is named
  ``obj.methodname``, where ``obj`` is some object (this may be an expression),
  and ``methodname`` is the name of a method that is defined by the object's type.
  Different types define different methods.  Methods of different types may have
  the same name without causing ambiguity.  (It is possible to define your own
  object types and methods, using *classes*, see :ref:`tut-classes`)
  The method :meth:`append` shown in the example is defined for list objects; it
  adds a new element at the end of the list.  In this example it is equivalent to
  ``result = result + [a]``, but more efficient.


.. _tut-defining:

Функц зарлах илүү дэлгэрэнгүй
=============================

Функц тодорхойлохдоо ялгаатай аргументууд өгөх боломжтой.
Ийм гурван хэлбэр байдаг, тэр нь хоорондоо хосолж болно.


.. _tut-defaultargs:

Default Argument Values
-----------------------

Хамгийн түгээмэл хэрэглэгддэг хэлбэр бол нэг эсвэл олон аргумент дээр анхны
утгыг нь тусгайлан зааж өгсөн хэлбэр юм.
Энэ нь функц үүсгэн функцийг дуудахад зарим аргументийг дамжуулахгүй
байж болно. Жишээлбэл::

   def ask_ok(prompt, retries=4, complaint='Yes or no, please!'):
       while True:
           ok = raw_input(prompt)
           if ok in ('y', 'ye', 'yes'):
               return True
           if ok in ('n', 'no', 'nop', 'nope'):
               return False
           retries = retries - 1
           if retries < 0:
               raise IOError('refusenik user')
           print complaint

Энэ функцийг олон янзаар дуудаж болно:

* зөвхөн зайлшгүй оруулах аргументийг өгөх:
  ``ask_ok('Do you really want to quit?')``
* оруулахгүй ч байж болох аргументийг өгөх:
  ``ask_ok('OK to overwrite the file?', 2)``
* эсвэл бүх аргументийг дамжуулах:
  ``ask_ok('OK to overwrite the file?', 2, 'Come on, only yes or no!')``

Энэ жишээн дээр :keyword:`in` түлхүүрийг үзүүлсэн. Энэ нь жагсаалт дотор
шалгах утга байгаа эсэхийг шалгана.

Анхны утгуудыг функцийн *зарлалтийн* хэсэгт утга дамжуулахгүй бол ямар 
утгатай байхыг заана.::

   i = 5

   def f(arg=i):
       print arg

   i = 6
   f()

``5`` -ыг хэвлэнэ.

**Чухал анхааруулга:**  Анхны утга бол нэг л удаа олгогдоно. Энэ анхны утга нь
хувирамтгай объект, дараалал, толь, эсвэл классын тохиолдлоос ялгаатай.
Жишээлбэл, дараах функцэд утга дамжуулан дахин дахин 
дуудвал нэг л удаа утга олгогдож жагсаалтын элемент нэмэгдэнэ::

   def f(a, L=[]):
       L.append(a)
       return L

   print f(1)
   print f(2)
   print f(3)

Үүнийг хэвлэнэ ::

   [1]
   [1, 2]
   [1, 2, 3]

Хэрэв та ийм үр дүн хүсэхгүй дуудах болгонд шинэ утга оноох бол 
дараах байдалтай бичнэ.::

   def f(a, L=None):
       if L is None:
           L = []
       L.append(a)
       return L


.. _tut-keywordargs:

Keyword Arguments
-----------------

Функцийг дуудахдаа форм аргументийг ашиглаж болно ``keyword =
value``.  Дараах функцийг авч үзье::

   def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
       print "-- This parrot wouldn't", action,
       print "if you put", voltage, "volts through it."
       print "-- Lovely plumage, the", type
       print "-- It's", state, "!"

дараах байдлаар функцийг дуудаж болно::

   parrot(1000)
   parrot(action = 'VOOOOOM', voltage = 1000000)
   parrot('a thousand', state = 'pushing up the daisies')
   parrot('a million', 'bereft of life', 'jump')

гэвч дараах дуудалтууд бүгд буруу::

   parrot()                     # аргумент дамжуулахыг шаардана
   parrot(voltage=5.0, 'dead')  # түлхүүргүй аргументад түлхүүр хэрэглэсэн
   parrot(110, voltage=220)     # аргументийн утгыг давхардуулсан
   parrot(actor='John Cleese')  # буруу түлхүүр

Ерөнхийдөө, аргументийн жагсаалт нь ямар нэг байрлалын аргументийг араас 
түлхүүр аргумент байрлана, түлхүүр аргументууд өгөхөд тодорхойлсон 
параметруудаас хайдаг. Үүнд тодорхойлсон параметрууд анхны утгатай байх 
эсвэл байхгүй нь нээх чухал биш. Ямар ч аргументгүй нэгээс олон удаа утга
ирвэл хэвжүүлсэн параметр нэрүүд нь байрлалын аргументийн түлхүүр шиг 
байрлалаар нь дуудаж чадахгүй. Энэ жишээн саяны нөхцөлөөр алдаа болснийг 
харуулав::

   >>> def function(a):
   ...     pass
   ...
   >>> function(0, a=0)
   Traceback (most recent call last):
     File "<stdin>", line 1, in ?
   TypeError: function() got multiple values for keyword argument 'a'

 Сүүлийн хэвжүүлсэн загвар дээр ``**name`` нэр заасан, энэ нь бүх түлхүүр 
 аргументийг багтаасан тольноос ирдэг(илүүг :ref:`typesmapping`).
 Энэ нь ``*name`` формын параметртэй нийлсэн байж болно.
(дараагийн дэд хэсэгт тайлбарласан) тэр нь байрлалын аргументийн оронд
хэвжүүлсэн параметрийн тапл жагсаалтын агуулсан байдаг.
(``*name`` энэн шиг байх ёстой ``**name``.) Жишээ, Хэрэв бид дараах
функцийг бичсэн бол::

   def cheeseshop(kind, *arguments, **keywords):
       print "-- Do you have any", kind, "?"
       print "-- I'm sorry, we're all out of", kind
       for arg in arguments: print arg
       print "-" * 40
       keys = keywords.keys()
       keys.sort()
       for kw in keys: print kw, ":", keywords[kw]

Үүн шиг дуудаж болно::

   cheeseshop("Limburger", "It's very runny, sir.",
              "It's really very, VERY runny, sir.",
              shopkeeper='Michael Palin',
              client="John Cleese",
              sketch="Cheese Shop Sketch")

мэдээж дараахийг хэвлэнэ::

   -- Do you have any Limburger ?
   -- I'm sorry, we're all out of Limburger
   It's very runny, sir.
   It's really very, VERY runny, sir.
   ----------------------------------------
   client : John Cleese
   shopkeeper : Michael Palin
   sketch : Cheese Shop Sketch

:meth:`sort` метод нь түлхүүр аргументуудийн нэрийг 
хэвлэхээсээ өмнө ``keywords`` толины агуулгыг эрэмбэлнэ; Хэрэв 
дуусаагүй байхад аргументууд хэвлэгдсэн бол энэ нь тодорхологдоогүй
гэсэн үг.


.. _tut-arbitraryargs:

Arbitrary Argument Lists
------------------------

.. index::
  statement: *

Эцэст нь хэлэхэд, бага давтамжтай хэрэглэгдэх функц дээр өөрийнхөө хүссэн 
хэмжээний аргументийг дамжуулж дуудаж болно.Эдгээр аргументууд нь нийлээд 
таплд байх ёстой(илүүг :ref:`tut-tuples`).  Олон тооны аргумент өгж болно,
өгөхгүй ч байж болно эсвэл энгийн аргумент өгж болно. ::

   def write_multiple_items(file, separator, *args):
       file.write(separator.join(args))


.. _tut-unpacking-arguments:

Unpacking Argument Lists
------------------------

Аргументууд аль хэдийн жагсаалт эсвэл тапл болсон байхад урвуу байрлал 
тохиолдоно, гэвч функцийг дуудахдаа байрлалын аргументуудыг задлаагүй 
байх хэрэгтэй. Зарим тохиолдолд ,  :func:`range` функц *start* болон
*stop* аргументуудыг салгахыг эсэргүүцдэг.Хэрвээ аргументууд нь саланги бол, 
функц бичихдээ ``*``\ -оператор ашиглан жагсаалт эсвэл тапл болгон 
нийлүүлнэ.::

   >>> range(3, 6)             # normal call with separate arguments
   [3, 4, 5]
   >>> args = [3, 6]
   >>> range(*args)            # call with arguments unpacked from a list
   [3, 4, 5]

.. index::
  statement: **

Үүнтэй адилаар түлхүүр аргументуудыг ``**``\
- оператор ашиглан тольнууд болгоно::

   >>> def parrot(voltage, state='a stiff', action='voom'):
   ...     print "-- This parrot wouldn't", action,
   ...     print "if you put", voltage, "volts through it.",
   ...     print "E's", state, "!"
   ...
   >>> d = {"voltage": "four million", "state": "bleedin' demised", "action": "VOOM"}
   >>> parrot(**d)
   -- This parrot wouldn't VOOM if you put four million volts through it. E's bleedin' demised !


.. _tut-lambda:

Lambda Forms
------------

By popular demand, a few features commonly found in functional programming
languages like Lisp have been added to Python.  With the :keyword:`lambda`
keyword, small anonymous functions can be created. Here's a function that
returns the sum of its two arguments: ``lambda a, b: a+b``.  Lambda forms can be
used wherever function objects are required.  They are syntactically restricted
to a single expression.  Semantically, they are just syntactic sugar for a
normal function definition.  Like nested function definitions, lambda forms can
reference variables from the containing scope::

   >>> def make_incrementor(n):
   ...     return lambda x: x + n
   ...
   >>> f = make_incrementor(42)
   >>> f(0)
   42
   >>> f(1)
   43


.. _tut-docstrings:

Documentation Strings
---------------------

.. index::
   single: docstrings
   single: documentation strings
   single: strings, documentation

There are emerging conventions about the content and formatting of documentation
strings.

The first line should always be a short, concise summary of the object's
purpose.  For brevity, it should not explicitly state the object's name or type,
since these are available by other means (except if the name happens to be a
verb describing a function's operation).  This line should begin with a capital
letter and end with a period.

If there are more lines in the documentation string, the second line should be
blank, visually separating the summary from the rest of the description.  The
following lines should be one or more paragraphs describing the object's calling
conventions, its side effects, etc.

The Python parser does not strip indentation from multi-line string literals in
Python, so tools that process documentation have to strip indentation if
desired.  This is done using the following convention. The first non-blank line
*after* the first line of the string determines the amount of indentation for
the entire documentation string.  (We can't use the first line since it is
generally adjacent to the string's opening quotes so its indentation is not
apparent in the string literal.)  Whitespace "equivalent" to this indentation is
then stripped from the start of all lines of the string.  Lines that are
indented less should not occur, but if they occur all their leading whitespace
should be stripped.  Equivalence of whitespace should be tested after expansion
of tabs (to 8 spaces, normally).

Here is an example of a multi-line docstring::

   >>> def my_function():
   ...     """Do nothing, but document it.
   ...
   ...     No, really, it doesn't do anything.
   ...     """
   ...     pass
   ...
   >>> print my_function.__doc__
   Do nothing, but document it.

       No, really, it doesn't do anything.


.. _tut-codingstyle:

Intermezzo: Coding Style
========================

.. sectionauthor:: Georg Brandl <georg@python.org>
.. index:: pair: coding; style

Бид Пайтоны тухай маш олон зүйлийг бичлээ ,харин одоо бид *код бичих загвар* -ийн
талаар ярилцах цаг болсон. Ихэнх хэлнүүд янз бүрийн (илүү товчилсон, *formatted*) загвараар бичигддэг; зарим нь илүү их бичиглэлтэй байдаг.
Код бичихдээ уншихад амархан байхаар бичих нь тохиромжтой байдаг, ба  
сайн кодын загвар сонгож авах нь таны хамгийн том амжилт байдаг.

Пайтонд зориулж, :pep:`8` загварыг хэлэлцэн ихэнх төсөлд ашигладаг;
энэ нь уншихад маш эвтэйхэн болон нүдэнд тустай кодын загвар юм. 
Пайтан хөгжүүлэгч болгон ямар ч цэгээс уншсан чухал зүйл нь хаана байгааг
мэдэж болно:

* 4 зай зэрэгцүүлэлт ашиглах болон ямар ч таб авахгүй.

  4 хоосон зай маш тохирсон жижиг зэрэгцүүлэлт (үргэлжилсэн гүнг зөвшөөрдөг) 
  болон том зэрэгцүүлэлт (уншихад амар).  Табууд нь төөрөлдөл үүсгэдэг.

* 79 тэмдэгтээс хэтрэхээс өмнө шинэ мөр ав.

  Хэрэглэгчид дэлгэцний том жижгээс хамаарахгүй эх кодыг мөр мөрөөр харуулахад
  хялбар байдаг.

* Функц класс болон их хэмжээний код, нэг утга илэрхийлэх блокуудыг хоосон
  мөрөөр заагла.

* Боломжтой бүх мөр дээр тайлбар хий.

* docstrings ашигла.

* Таслал болон операторуудын ард хоосон зай ашигла, гэвч хаалттай байгуулагч
  хэрэглэж болохгүй: ``a = f(1, 2) + g(3, 4)``.

* Класс болон функцын нэрээ тогтвортойгоор нэрлэ; Классуудад ``CamelCase`` 
  стандарт болон функц методууддаа ``lower_case_with_underscores`` стандарт
  ашигла. Методын эхний аргумент байнга  ``self`` аргумент ашигла.
  (Класс методын дэлгэрэнгүйг :ref:`tut-firstclasses`-ээс үз ).

* Хэлний нэмэгдэл орчин ашиглан олон улсын энкод кодондоо ашиглах хэрэггүй.
  Энгийн ASCII works best in any case.


.. rubric:: Footnotes

.. [#] Actually, *call by object reference* would be a better description,
   since if a mutable object is passed, the caller will see any changes the
   callee makes to it (items inserted into a list).

