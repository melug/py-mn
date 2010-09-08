.. _tut-brieftour:

***********************************
Стандарт сангуудаар хийх товч аялал
***********************************


.. _tut-os-interface:

Үйлдлийн системийн интерфэйс
==========================

:mod:`os` модуль нь үйлдлийн системтэй ажиллах олон тооны функцуудыг агуулдаг.

   >>> import os
   >>> os.system('time 0:02')
   0
   >>> os.getcwd()      # Одоо ажиллаж буй хавтсыг буцаана
   'C:\\Python26'
   >>> os.chdir('/server/accesslogs')

Гэхдээ ``from os import *`` гэхийн оронд ``import os``-ийг хэрэглэж заншаарай. Энэ нь :func:`os.open` функцээр огт өөрөөр ажилладаг :func:`open` функцыг сүүдэрлэхээс хамгаалах болно.

.. index:: builtin: help

Пайтоны :func:`dir` болон :func:`help` функцүүд нь :mod:`os`:: мэт том модулиудтай ажиллаж байхад интерактив туслалцаа авахад тустай байдаг.

   >>> import os
   >>> dir(os)
   <модуль дахь бүх функцүүдийн жагсаалтыг буцаана>
   >>> help(os)
   <модулийн docstring-с үүсгэсэн дэлгэрэнгүй гарын авлагыг буцаана>

Өдөр тутмын файл болон хавтастай ажиллах тохиолдолд :mod:`shutil` нь ашиглахад хялбар илүү өндөр түвшний интерфэйс юм::

   >>> import shutil
   >>> shutil.copyfile('data.db', 'archive.db')
   >>> shutil.move('/build/executables', 'installdir')


.. _tut-file-wildcards:

Файлын Wildcards
==============

:mod:`glob` модуль нь хавтаснаас wildcard хайлтаар файлуудын жагсаалт үүсгэх функцийг агуулдаг::

   >>> import glob
   >>> glob.glob('*.py')
   ['primes.py', 'random.py', 'quote.py']


.. _tut-command-line-arguments:

Command Line Arguments
======================

Common utility scripts often need to process command line arguments. These
arguments are stored in the :mod:`sys` module's *argv* attribute as a list.  For
instance the following output results from running ``python demo.py one two
three`` at the command line::

   >>> import sys
   >>> print sys.argv
   ['demo.py', 'one', 'two', 'three']

The :mod:`getopt` module processes *sys.argv* using the conventions of the Unix
:func:`getopt` function.  More powerful and flexible command line processing is
provided by the :mod:`argparse` module.


.. _tut-stderr:

Error Output Redirection and Program Termination
================================================

The :mod:`sys` module also has attributes for *stdin*, *stdout*, and *stderr*.
The latter is useful for emitting warnings and error messages to make them
visible even when *stdout* has been redirected::

   >>> sys.stderr.write('Warning, log file not found starting a new one\n')
   Warning, log file not found starting a new one

The most direct way to terminate a script is to use ``sys.exit()``.


.. _tut-string-pattern-matching:

String Pattern Matching
=======================

The :mod:`re` module provides regular expression tools for advanced string
processing. For complex matching and manipulation, regular expressions offer
succinct, optimized solutions::

   >>> import re
   >>> re.findall(r'\bf[a-z]*', 'which foot or hand fell fastest')
   ['foot', 'fell', 'fastest']
   >>> re.sub(r'(\b[a-z]+) \1', r'\1', 'cat in the the hat')
   'cat in the hat'

When only simple capabilities are needed, string methods are preferred because
they are easier to read and debug::

   >>> 'tea for too'.replace('too', 'two')
   'tea for two'


.. _tut-mathematics:

Mathematics
===========

The :mod:`math` module gives access to the underlying C library functions for
floating point math::

   >>> import math
   >>> math.cos(math.pi / 4.0)
   0.70710678118654757
   >>> math.log(1024, 2)
   10.0

The :mod:`random` module provides tools for making random selections::

   >>> import random
   >>> random.choice(['apple', 'pear', 'banana'])
   'apple'
   >>> random.sample(xrange(100), 10)   # sampling without replacement
   [30, 83, 16, 4, 8, 81, 41, 50, 18, 33]
   >>> random.random()    # random float
   0.17970987693706186
   >>> random.randrange(6)    # random integer chosen from range(6)
   4


.. _tut-internet-access:

Internet Access
===============

There are a number of modules for accessing the internet and processing internet
protocols. Two of the simplest are :mod:`urllib2` for retrieving data from urls
and :mod:`smtplib` for sending mail::

   >>> import urllib2
   >>> for line in urllib2.urlopen('http://tycho.usno.navy.mil/cgi-bin/timer.pl'):
   ...     if 'EST' in line or 'EDT' in line:  # look for Eastern Time
   ...         print line

   <BR>Nov. 25, 09:43:32 PM EST

   >>> import smtplib
   >>> server = smtplib.SMTP('localhost')
   >>> server.sendmail('soothsayer@example.org', 'jcaesar@example.org',
   ... """To: jcaesar@example.org
   ... From: soothsayer@example.org
   ...
   ... Beware the Ides of March.
   ... """)
   >>> server.quit()

(Note that the second example needs a mailserver running on localhost.)


.. _tut-dates-and-times:

Огноо болон цаг
===============

The :mod:`datetime` module supplies classes for manipulating dates and times in
both simple and complex ways. While date and time arithmetic is supported, the
focus of the implementation is on efficient member extraction for output
formatting and manipulation.  The module also supports objects that are timezone
aware. ::

   >>> # dates are easily constructed and formatted
   >>> from datetime import date
   >>> now = date.today()
   >>> now
   datetime.date(2003, 12, 2)
   >>> now.strftime("%m-%d-%y. %d %b %Y is a %A on the %d day of %B.")
   '12-02-03. 02 Dec 2003 is a Tuesday on the 02 day of December.'

   >>> # dates support calendar arithmetic
   >>> birthday = date(1964, 7, 31)
   >>> age = now - birthday
   >>> age.days
   14368


.. _tut-data-compression:

Өгөгдөл шахах
=============

:mod:`zlib`, :mod:`gzip`, :mod:`bz2`, :mod:`zipfile` болон
:mod:`tarfile` зэрэг модулиуд нь өгөгдлийг архивлах болон шахах түгээмэл форматуудыг дэмждэг ::

   >>> import zlib
   >>> s = 'witch which has which witches wrist watch'
   >>> len(s)
   41
   >>> t = zlib.compress(s)
   >>> len(t)
   37
   >>> zlib.decompress(t)
   'witch which has which witches wrist watch'
   >>> zlib.crc32(s)
   226805979


.. _tut-performance-measurement:

Performance Measurement
=======================

Some Python users develop a deep interest in knowing the relative performance of
different approaches to the same problem. Python provides a measurement tool
that answers those questions immediately.

For example, it may be tempting to use the tuple packing and unpacking feature
instead of the traditional approach to swapping arguments. The :mod:`timeit`
module quickly demonstrates a modest performance advantage::

   >>> from timeit import Timer
   >>> Timer('t=a; a=b; b=t', 'a=1; b=2').timeit()
   0.57535828626024577
   >>> Timer('a,b = b,a', 'a=1; b=2').timeit()
   0.54962537085770791

In contrast to :mod:`timeit`'s fine level of granularity, the :mod:`profile` and
:mod:`pstats` modules provide tools for identifying time critical sections in
larger blocks of code.


.. _tut-quality-control:

Чанарын удирдлага
=================

One approach for developing high quality software is to write tests for each
function as it is developed and to run those tests frequently during the
development process.

The :mod:`doctest` module provides a tool for scanning a module and validating
tests embedded in a program's docstrings.  Test construction is as simple as
cutting-and-pasting a typical call along with its results into the docstring.
This improves the documentation by providing the user with an example and it
allows the doctest module to make sure the code remains true to the
documentation::

   def average(values):
       """Computes the arithmetic mean of a list of numbers.

       >>> print average([20, 30, 70])
       40.0
       """
       return sum(values, 0.0) / len(values)

   import doctest
   doctest.testmod()   # automatically validate the embedded tests

The :mod:`unittest` module is not as effortless as the :mod:`doctest` module,
but it allows a more comprehensive set of tests to be maintained in a separate
file::

   import unittest

   class TestStatisticalFunctions(unittest.TestCase):

       def test_average(self):
           self.assertEqual(average([20, 30, 70]), 40.0)
           self.assertEqual(round(average([1, 5, 7]), 1), 4.3)
           self.assertRaises(ZeroDivisionError, average, [])
           self.assertRaises(TypeError, average, 20, 30, 70)

   unittest.main() # Calling from the command line invokes all tests


.. _tut-batteries-included:

Batteries Included
==================

Python has a "batteries included" philosophy.  This is best seen through the
sophisticated and robust capabilities of its larger packages. For example:

* The :mod:`xmlrpclib` and :mod:`SimpleXMLRPCServer` modules make implementing
  remote procedure calls into an almost trivial task.  Despite the modules
  names, no direct knowledge or handling of XML is needed.

* The :mod:`email` package is a library for managing email messages, including
  MIME and other RFC 2822-based message documents. Unlike :mod:`smtplib` and
  :mod:`poplib` which actually send and receive messages, the email package has
  a complete toolset for building or decoding complex message structures
  (including attachments) and for implementing internet encoding and header
  protocols.

* The :mod:`xml.dom` and :mod:`xml.sax` packages provide robust support for
  parsing this popular data interchange format. Likewise, the :mod:`csv` module
  supports direct reads and writes in a common database format. Together, these
  modules and packages greatly simplify data interchange between Python
  applications and other tools.

* Internationalization is supported by a number of modules including
  :mod:`gettext`, :mod:`locale`, and the :mod:`codecs` package.


