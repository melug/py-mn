.. _tut-errors:

*********************
Errors and Exceptions
*********************

Until now error messages haven't been more than mentioned, but if you have tried
out the examples you have probably seen some.  There are (at least) two
distinguishable kinds of errors: *syntax errors* and *exceptions*.


.. _tut-syntaxerrors:

Syntax Errors
=============

Синтаксийн алдаанууд нь хөрвүүлэх алдаа ч гэдэг, Пайтон сурж эхэлж байхад
нийтлэг тохиолддог::

   >>> while True print 'Hello world'
     File "<stdin>", line 1, in ?
       while True print 'Hello world'
                      ^
   SyntaxError: invalid syntax

Хөрвүүлэгч нь алдаатай мөрийн доогуур сумаар заадаг бөгөөд хамгийн анхны
алдаа гарангуут алдааг үзүүлдэг. Алдаа нь заасан сумаас урагшаа буруу зүйл
хийснээр болдог(эсвэл сумны ойролцоо): жишээн дээр, алдаа нь :keyword:`print`
түлхүүр үгний ойролцоо гарсан бөгөөд өмнө нь (``':'``) бичихээ мартсан байна.
Кодыг скрипт байдлаар ажиллуулсан тохиолдолд файлын нэр болон мөрийн дугаар
хэвлэгддэг бөгөөд ямар алдаа хаана гарсныг нь мэдэж болно.


.. _tut-exceptions:

Exceptions
==========

Илэрхийлэл болон бичиглэл нь синтаксийн ямар нэг алдаагүй боловч ажиллуулах
үед алдаа гарч болно.Алдаанууд нь ажиллах явцад гарах алдааг *онцгой тохиодол*
гэх бөгөөд боломжийг тооцож үзээгүй бол гарна: та удахгүй эдгээр алдааг хэрхэн
Пайтон програмд хэрхэн барих талаар үзнэ. Ихэнх онцгой тохиолдлууд нь програм
дээр баригдаагүй байдаг учир үр дүнд нь доор үзүүлсэн шиг алдааний мэдээллүүд
гардаг байна::

   >>> 10 * (1/0)
   Traceback (most recent call last):
     File "<stdin>", line 1, in ?
   ZeroDivisionError: integer division or modulo by zero
   >>> 4 + spam*3
   Traceback (most recent call last):
     File "<stdin>", line 1, in ?
   NameError: name 'spam' is not defined
   >>> '2' + 2
   Traceback (most recent call last):
     File "<stdin>", line 1, in ?
   TypeError: cannot concatenate 'str' and 'int' objects

Сүүлийн мөр дээр алдааний мэдээлэл нь юу болснийг заасан байна. Онцгой тохиолдлууд
ялгаатай төрөлтэй байдаг, тэр төрөл нь алдааний мэдээллийн хэсэг болж гардаг:
жишээн дээр :exc:`ZeroDivisionError`, :exc:`NameError` болон :exc:`TypeError`
төрлийн онцгой тохиолдлууд гарсан байна. Тодорхойлогдсон байдаг онцгой тохиолдлын
төрөл нь хэвлэгддэг. Энэ нь бүх тодорхойлогдсон онцгой тохиолдлууд дээр хэрэгждэг
ба хэрэглэгчийн тодорхойлсон онцгой тохиолдол дээр худал утга гаргаж болно.
Стандарт онцгой тохиолдлын нэрүүд нь танигчаар тодорхойлогдоно.( түлхүүр үг
нөөцлөдөггүй)

Алдааны мөр нь онцгой тохиолдлын төрөл дээр суурилан юунаас болж энэ алдаа
гарсан гэдгийг дэлгэрэнгүй харуулах боломжийг олгодог.

Алдааны мэдээллийн өмнөх хэсэг нь хаана онцгой тохиолдол гарсныг заадаг ба
араас нь стек трэс үзүүлдэг. Ерөнхийдөө эх кодын мөрүүд нь стэк трэсбак агуулдаг
ч гэсэн стандарт оролтоос уншсаныг дэлгэцэнд харуулдаггүй.

:ref:`bltin-exceptions` тодорхойлогдсон онцгой тохиолдлууд болон тэдгээрийн 
утгыг харж болно.


.. _tut-handling:

Алдаа барих
===========

Програм бичихдээ сонгогдсон онцгой тохиолдлыг барих боломжтой байдаг. Дараах
жишээнээс харахад хэрэглэгч оролтоос буруу тоо оруулахад програм алдаа өгөн
ажиллагааг зогсоож байна(:kbd:`Control-C` эсвэл ямар нэг үйлдлийн системийн
үйлдэл хийхэд мөн энэ алдаа гарна) хэрэглэгчийн үүсгэсэн тасалдуулах ажиллагаа
нь :exc:`KeyboardInterrupt` онцгой тохиолдлыг дуудна.::

   >>> while True:
   ...     try:
   ...         x = int(raw_input("Please enter a number: "))
   ...         break
   ...     except ValueError:
   ...         print "Oops!  That was no valid number.  Try again..."
   ...

:keyword:`try` илэрхийлэл нь дараах зарчмаар ажиллана.

* Эхлээд, *try нөхцөл* (:keyword:`try` ба :keyword:`except` түлхүүр үгийн
  хоорондох код) ажиллана.

* Хэрэв ямар ч онцгой тохиолдол байхгүй бол *except нөхцөл* -ыг алгасан 
  ажиллах бөгөөд :keyword:`try` илэрхийлэл дуусна.

* Хэрэв try хэсгээс ямар нэг алдаа гарвал алдаа гарснаас доод хэсгийн кодыг алгасна.
  Тэгээд гарсан алдаанд таарсан төрөл :keyword:`except` хэсэг дээр очно, except 
  хэсэг ажиллаж ба ажилласны дараа үргэлжлэн :keyword:`try` илэрхийллийн зогссон
  газраас ажиллаж эхэлнэ.

* Хэрэв гарсан алдаа нь алдаа барилт дотор байхгүй бол :keyword:`try` илэрхийллээс гаран
  ямар алдаа барилт олдоогүй тул  *unhandled exception* гэдэг мэдээлэл гарган ажиллагааг
  зогсооно.

A :keyword:`try` statement may have more than one except clause, to specify
handlers for different exceptions.  At most one handler will be executed.
Handlers only handle exceptions that occur in the corresponding try clause, not
in other handlers of the same :keyword:`try` statement.  An except clause may
name multiple exceptions as a parenthesized tuple, for example::

   ... except (RuntimeError, TypeError, NameError):
   ...     pass

The last except clause may omit the exception name(s), to serve as a wildcard.
Use this with extreme caution, since it is easy to mask a real programming error
in this way!  It can also be used to print an error message and then re-raise
the exception (allowing a caller to handle the exception as well)::

   import sys

   try:
       f = open('myfile.txt')
       s = f.readline()
       i = int(s.strip())
   except IOError as (errno, strerror):
       print "I/O error({0}): {1}".format(errno, strerror)
   except ValueError:
       print "Could not convert data to an integer."
   except:
       print "Unexpected error:", sys.exc_info()[0]
       raise

The :keyword:`try` ... :keyword:`except` statement has an optional *else
clause*, which, when present, must follow all except clauses.  It is useful for
code that must be executed if the try clause does not raise an exception.  For
example::

   for arg in sys.argv[1:]:
       try:
           f = open(arg, 'r')
       except IOError:
           print 'cannot open', arg
       else:
           print arg, 'has', len(f.readlines()), 'lines'
           f.close()

The use of the :keyword:`else` clause is better than adding additional code to
the :keyword:`try` clause because it avoids accidentally catching an exception
that wasn't raised by the code being protected by the :keyword:`try` ...
:keyword:`except` statement.

When an exception occurs, it may have an associated value, also known as the
exception's *argument*. The presence and type of the argument depend on the
exception type.

The except clause may specify a variable after the exception name (or tuple).
The variable is bound to an exception instance with the arguments stored in
``instance.args``.  For convenience, the exception instance defines
:meth:`__str__` so the arguments can be printed directly without having to
reference ``.args``.

One may also instantiate an exception first before raising it and add any
attributes to it as desired. ::

   >>> try:
   ...    raise Exception('spam', 'eggs')
   ... except Exception as inst:
   ...    print type(inst)     # the exception instance
   ...    print inst.args      # arguments stored in .args
   ...    print inst           # __str__ allows args to printed directly
   ...    x, y = inst          # __getitem__ allows args to be unpacked directly
   ...    print 'x =', x
   ...    print 'y =', y
   ...
   <type 'exceptions.Exception'>
   ('spam', 'eggs')
   ('spam', 'eggs')
   x = spam
   y = eggs

If an exception has an argument, it is printed as the last part ('detail') of
the message for unhandled exceptions.

Exception handlers don't just handle exceptions if they occur immediately in the
try clause, but also if they occur inside functions that are called (even
indirectly) in the try clause. For example::

   >>> def this_fails():
   ...     x = 1/0
   ...
   >>> try:
   ...     this_fails()
   ... except ZeroDivisionError as detail:
   ...     print 'Handling run-time error:', detail
   ...
   Handling run-time error: integer division or modulo by zero


.. _tut-raising:

Raising Exceptions
==================

The :keyword:`raise` statement allows the programmer to force a specified
exception to occur. For example::

   >>> raise NameError('HiThere')
   Traceback (most recent call last):
     File "<stdin>", line 1, in ?
   NameError: HiThere

The sole argument to :keyword:`raise` indicates the exception to be raised.
This must be either an exception instance or an exception class (a class that
derives from :class:`Exception`).

If you need to determine whether an exception was raised but don't intend to
handle it, a simpler form of the :keyword:`raise` statement allows you to
re-raise the exception::

   >>> try:
   ...     raise NameError('HiThere')
   ... except NameError:
   ...     print 'An exception flew by!'
   ...     raise
   ...
   An exception flew by!
   Traceback (most recent call last):
     File "<stdin>", line 2, in ?
   NameError: HiThere


.. _tut-userexceptions:

User-defined Exceptions
=======================

Programs may name their own exceptions by creating a new exception class (see
:ref:`tut-classes` for more about Python classes).  Exceptions should typically
be derived from the :exc:`Exception` class, either directly or indirectly.  For
example::

   >>> class MyError(Exception):
   ...     def __init__(self, value):
   ...         self.value = value
   ...     def __str__(self):
   ...         return repr(self.value)
   ...
   >>> try:
   ...     raise MyError(2*2)
   ... except MyError as e:
   ...     print 'My exception occurred, value:', e.value
   ...
   My exception occurred, value: 4
   >>> raise MyError('oops!')
   Traceback (most recent call last):
     File "<stdin>", line 1, in ?
   __main__.MyError: 'oops!'

In this example, the default :meth:`__init__` of :class:`Exception` has been
overridden.  The new behavior simply creates the *value* attribute.  This
replaces the default behavior of creating the *args* attribute.

Exception classes can be defined which do anything any other class can do, but
are usually kept simple, often only offering a number of attributes that allow
information about the error to be extracted by handlers for the exception.  When
creating a module that can raise several distinct errors, a common practice is
to create a base class for exceptions defined by that module, and subclass that
to create specific exception classes for different error conditions::

   class Error(Exception):
       """Base class for exceptions in this module."""
       pass

   class InputError(Error):
       """Exception raised for errors in the input.

       Attributes:
           expr -- input expression in which the error occurred
           msg  -- explanation of the error
       """

       def __init__(self, expr, msg):
           self.expr = expr
           self.msg = msg

   class TransitionError(Error):
       """Raised when an operation attempts a state transition that's not
       allowed.

       Attributes:
           prev -- state at beginning of transition
           next -- attempted new state
           msg  -- explanation of why the specific transition is not allowed
       """

       def __init__(self, prev, next, msg):
           self.prev = prev
           self.next = next
           self.msg = msg

Most exceptions are defined with names that end in "Error," similar to the
naming of the standard exceptions.

Many standard modules define their own exceptions to report errors that may
occur in functions they define.  More information on classes is presented in
chapter :ref:`tut-classes`.


.. _tut-cleanup:

Defining Clean-up Actions
=========================

The :keyword:`try` statement has another optional clause which is intended to
define clean-up actions that must be executed under all circumstances.  For
example::

   >>> try:
   ...     raise KeyboardInterrupt
   ... finally:
   ...     print 'Goodbye, world!'
   ...
   Goodbye, world!
   Traceback (most recent call last):
     File "<stdin>", line 2, in ?
   KeyboardInterrupt

A *finally clause* is always executed before leaving the :keyword:`try`
statement, whether an exception has occurred or not. When an exception has
occurred in the :keyword:`try` clause and has not been handled by an
:keyword:`except` clause (or it has occurred in a :keyword:`except` or
:keyword:`else` clause), it is re-raised after the :keyword:`finally` clause has
been executed.  The :keyword:`finally` clause is also executed "on the way out"
when any other clause of the :keyword:`try` statement is left via a
:keyword:`break`, :keyword:`continue` or :keyword:`return` statement.  A more
complicated example (having :keyword:`except` and :keyword:`finally` clauses in
the same :keyword:`try` statement works as of Python 2.5)::

   >>> def divide(x, y):
   ...     try:
   ...         result = x / y
   ...     except ZeroDivisionError:
   ...         print "division by zero!"
   ...     else:
   ...         print "result is", result
   ...     finally:
   ...         print "executing finally clause"
   ...
   >>> divide(2, 1)
   result is 2
   executing finally clause
   >>> divide(2, 0)
   division by zero!
   executing finally clause
   >>> divide("2", "1")
   executing finally clause
   Traceback (most recent call last):
     File "<stdin>", line 1, in ?
     File "<stdin>", line 3, in divide
   TypeError: unsupported operand type(s) for /: 'str' and 'str'

As you can see, the :keyword:`finally` clause is executed in any event.  The
:exc:`TypeError` raised by dividing two strings is not handled by the
:keyword:`except` clause and therefore re-raised after the :keyword:`finally`
clause has been executed.

In real world applications, the :keyword:`finally` clause is useful for
releasing external resources (such as files or network connections), regardless
of whether the use of the resource was successful.


.. _tut-cleanup-with:

Predefined Clean-up Actions
===========================

Some objects define standard clean-up actions to be undertaken when the object
is no longer needed, regardless of whether or not the operation using the object
succeeded or failed. Look at the following example, which tries to open a file
and print its contents to the screen. ::

   for line in open("myfile.txt"):
       print line

The problem with this code is that it leaves the file open for an indeterminate
amount of time after the code has finished executing. This is not an issue in
simple scripts, but can be a problem for larger applications. The
:keyword:`with` statement allows objects like files to be used in a way that
ensures they are always cleaned up promptly and correctly. ::

   with open("myfile.txt") as f:
       for line in f:
           print line

After the statement is executed, the file *f* is always closed, even if a
problem was encountered while processing the lines. Other objects which provide
predefined clean-up actions will indicate this in their documentation.


