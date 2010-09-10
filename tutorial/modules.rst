.. _tut-modules:

*******
Modules
*******

Хэрвээ та пайтон хэлмэрчээс(interpreter)гараад буцаад ороход таны 
тодорхойлолтууд(функцууд болон хувьсагчууд) арчигдана. Тийм учраас,
Хэрэв та ямар нэг багагүй хэмжээтэй програм бичих бол, өөрийн сайн 
эзэмшсэн текст засварлагч дээрээ кодоо бичих бөгөөд тэр бичсэн кодын
файлаа хэлмэрч руу оролт болгон дамжуулах нь гараас код бичихээс илүү
найдвартай юм.Үүнийг *бичиглэл* үүсгэх гэж хэлнэ.Таны програм хэтэрхий
нүсэр болон, засвар үйлчилгээ авахад хялбар болгох зорилгоор та олон 
файлуудад салгаж болно.  Та магадгүй байнга хэрэглэдэг функцээ програм
бүрд дахин дахин хуулж тавилгүйгээр эвтэйхэн болгохыг хүсэж болно.

Иймэрхүү асуудлуудыг шийдэхийн тулд, Пайтон нь файлд тодорхойлолтууд нэмэн
түүнийгээ скрипт болгон ашиглах эсвэл харилцуурын тохиолдол болгодог. Файлыг
*module* болгон дууддаг; тодорхойлолтуудыг үндсэн болон бусад туслах модулиудаас
*импортлож* чаддаг.(хувьсагчдын цуглуулга нь дээд түвшний скрипт гүйцэтгэхэд
болон тооцоолох горимд хийх боломж олгодог).

Модуль бол пайтон тодорхойлолт болон илэрхийллийг агуулдаг. Файлын нэр нь 
модулийн нэрийн араас :file:`.py` дагавар залгагддаг. Модулын дотор модулийн
нэрийг илэрхийлдэг(тэмдэгтээр) ``__name__`` глобаль хувьсагч байдаг. Жишээ нь 
та өөрийн хэрэглэдэг текст засварлагч ашиглан дараах кодыг өөрийн ажиллаж байгаа
директорт :file:`fibo.py` нэртэйгээр үүсгэн хадгал::

   # Fibonacci numbers module

   def fib(n):    # write Fibonacci series up to n
       a, b = 0, 1
       while b < n:
           print b,
           a, b = b, a+b

   def fib2(n): # return Fibonacci series up to n
       result = []
       a, b = 0, 1
       while b < n:
           result.append(b)
           a, b = b, a+b
       return result

Одоо Пайтан хэлмэрч руу орон дараах командаар энэ модулыг импортлоно.::

   >>> import fibo

Энд ``fibo`` дотор тодорхойлсон функцийн тодорхойлолтын нэрийг бичээгүй ч гэсэн
тэмдэгтийн хүснэгтээр хайдаг, зөвхөн ``fibo`` модулын нэрээр хандана. Модулын
нэрээр хандан функцийг дуудахыг дор үзүүлэв::

   >>> fibo.fib(1000)
   1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
   >>> fibo.fib2(100)
   [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
   >>> fibo.__name__
   'fibo'

Хэрэв чи функцээ олон газар ашиглах бол локал нэр оноож болно::

   >>> fib = fibo.fib
   >>> fib(500)
   1 1 2 3 5 8 13 21 34 55 89 144 233 377


.. _tut-moremodules:

More on Modules
===============

Модуль нь функцийн тодорхойлолтоос гадна ажиллах боломжтой илэрхийллийг 
агуулж чадна.Эдгээр илэрхийлэлүүд нь модульд утга оноох үүрэгтэй.  Эдгээр
нь модулийг хаа нэг газар *анх удаа* импортлоход ажилладаг.[#]_

Модуль өөрийн гэсэн тэмдэгтийн хүснэгт эзэмшдэг, энэхүү хүснэгт нь глобаль 
тэмдэгтийн хүснэгтийн модуль дахь бүх функцийн тодорхойлолтийг хэрэглэдэг.
Энэ нь модулийн зохиогчид модуль дахь глобаль хувьсагчдыг хэрэглэгчдийн
глобаль хувьсагчидтай зөрчилдөхийг санаа тавьдаг. Өөрөөр хэлбэл, хэрвээ чи
юу хийхээ мэдэж байвал модулийнхаа глобаль хувьсагчтай ижил тэмдэглэгээг 
хэрэглэж болох бөгөөд энэ нь ``modname.itemname`` функцдээ хамааралтай байх
ёстой.

Модулиуд бусад модулиудийг импортлож чадна. Энэ бол ердийн л зүйл гэвч 
:keyword:`import` илэрхийллүүдийг заавал модулийн эхэнд(эсвэл скриптийн
эхэнд, за өөр хаана ч) бичих шаардлагагүй. Импортлогдсон модулийн нэр нь 
импортлож байгаа модулийн глобаль тэмдэгтийн хүснэгтэд байрладаг.

:keyword:`import` илэрхийллийн онцлог бол импортийн нэрүүд нь импортлож байгаа
модулийн тэмдэгтийн хүснэгтээс шууд авдаг. Жишээ нь::

   >>> from fibo import fib, fib2
   >>> fib(500)
   1 1 2 3 5 8 13 21 34 55 89 144 233 377

Энэ нь модулийг импортлохдоо модулийн нэрийг мэдэж чадахгүй учир локаль
тэмдэгтийн хүснэгтээр харж импортлоно.(жишээн дээр ``fibo`` тодорхойлогдоогүй)

Дараах илэрхийллээр модуль доторх бүх тодорхойлолт нэрүүдийг авна::

   >>> from fibo import *
   >>> fib(500)
   1 1 2 3 5 8 13 21 34 55 89 144 233 377

Бүх нэрийг импортлохдоо (``_``)-аар эхэлсэнүүдийг нь алгасна.

Ер нь бол багч эсвэл модулийг импортлохдоо ``*`` гэж хэрэглэдэг ерөнхий 
туршлагыг зөвшөөрдөггүй байсан ч уншихад эвтэйхэн болгохын тулд зөвшөөрсөн.
Гэсэн хэдий ч интерактив горимд ингэж бичихэд ямар ч асуудалгүй.

.. note::

   Үр ашигтай байлгахын тулд модулийг интерпретерийн тохиолдол бүр дээр нэг л 
   удаа импортлогддог. Ингэснээр, хэрвээ чи өөрийн модулийг өөрчлөх бол 
   интерпретерийг дахин ачалаах хэрэгтэй -- эсвэл :func:`reload` функцийг 
   ашиглан дахин ачаалж болно. ``reload(modulename)`` гэх мэт.


.. _tut-modulesasscripts:

Executing modules as scripts
----------------------------

Пайтон модулийг ажиллуулахдаа ::

   python fibo.py <arguments>

ингэснээр таны хүссэн кодын модуль ажиллана , гэвч бид 
``__name__`` -д ``"__main__"`` гэж тохируулж өгнө. Үүнийг 
ажиллуулахын тулд дараах кодыг мөрийн төгсгөлд нэмж болно::

   if __name__ == "__main__":
       import sys
       fib(int(sys.argv[1]))

ингэснээр та илүү хэрэглэхэд хялбар мөн импортлогдох боломжтой бөгөөд,
командийн мөрөөс үндсэн файлыг ажиллуулахад ч гэсэн ямар ч асуудалгүй::

   $ python fibo.py 50
   1 1 2 3 5 8 13 21 34

Кодыг импортлоход код ажиллахгүй::

   >>> import fibo
   >>>


.. _tut-searchpath:

The Module Search Path
----------------------

.. index:: triple: module; search; path

When a module named :mod:`spam` is imported, the interpreter searches for a file
named :file:`spam.py` in the current directory, and then in the list of
directories specified by the environment variable :envvar:`PYTHONPATH`.  This
has the same syntax as the shell variable :envvar:`PATH`, that is, a list of
directory names.  When :envvar:`PYTHONPATH` is not set, or when the file is not
found there, the search continues in an installation-dependent default path; on
Unix, this is usually :file:`.:/usr/local/lib/python`.

Actually, modules are searched in the list of directories given by the variable
``sys.path`` which is initialized from the directory containing the input script
(or the current directory), :envvar:`PYTHONPATH` and the installation- dependent
default.  This allows Python programs that know what they're doing to modify or
replace the module search path.  Note that because the directory containing the
script being run is on the search path, it is important that the script not have
the same name as a standard module, or Python will attempt to load the script as
a module when that module is imported. This will generally be an error.  See
section :ref:`tut-standardmodules` for more information.


"Compiled" Python files
-----------------------

As an important speed-up of the start-up time for short programs that use a lot
of standard modules, if a file called :file:`spam.pyc` exists in the directory
where :file:`spam.py` is found, this is assumed to contain an
already-"byte-compiled" version of the module :mod:`spam`. The modification time
of the version of :file:`spam.py` used to create :file:`spam.pyc` is recorded in
:file:`spam.pyc`, and the :file:`.pyc` file is ignored if these don't match.

Normally, you don't need to do anything to create the :file:`spam.pyc` file.
Whenever :file:`spam.py` is successfully compiled, an attempt is made to write
the compiled version to :file:`spam.pyc`.  It is not an error if this attempt
fails; if for any reason the file is not written completely, the resulting
:file:`spam.pyc` file will be recognized as invalid and thus ignored later.  The
contents of the :file:`spam.pyc` file are platform independent, so a Python
module directory can be shared by machines of different architectures.

Some tips for experts:

* When the Python interpreter is invoked with the :option:`-O` flag, optimized
  code is generated and stored in :file:`.pyo` files.  The optimizer currently
  doesn't help much; it only removes :keyword:`assert` statements.  When
  :option:`-O` is used, *all* :term:`bytecode` is optimized; ``.pyc`` files are
  ignored and ``.py`` files are compiled to optimized bytecode.

* Passing two :option:`-O` flags to the Python interpreter (:option:`-OO`) will
  cause the bytecode compiler to perform optimizations that could in some rare
  cases result in malfunctioning programs.  Currently only ``__doc__`` strings are
  removed from the bytecode, resulting in more compact :file:`.pyo` files.  Since
  some programs may rely on having these available, you should only use this
  option if you know what you're doing.

* A program doesn't run any faster when it is read from a :file:`.pyc` or
  :file:`.pyo` file than when it is read from a :file:`.py` file; the only thing
  that's faster about :file:`.pyc` or :file:`.pyo` files is the speed with which
  they are loaded.

* When a script is run by giving its name on the command line, the bytecode for
  the script is never written to a :file:`.pyc` or :file:`.pyo` file.  Thus, the
  startup time of a script may be reduced by moving most of its code to a module
  and having a small bootstrap script that imports that module.  It is also
  possible to name a :file:`.pyc` or :file:`.pyo` file directly on the command
  line.

* It is possible to have a file called :file:`spam.pyc` (or :file:`spam.pyo`
  when :option:`-O` is used) without a file :file:`spam.py` for the same module.
  This can be used to distribute a library of Python code in a form that is
  moderately hard to reverse engineer.

  .. index:: module: compileall

* The module :mod:`compileall` can create :file:`.pyc` files (or :file:`.pyo`
  files when :option:`-O` is used) for all modules in a directory.


.. _tut-standardmodules:

Standard Modules
================

.. index:: module: sys

Python comes with a library of standard modules, described in a separate
document, the Python Library Reference ("Library Reference" hereafter).  Some
modules are built into the interpreter; these provide access to operations that
are not part of the core of the language but are nevertheless built in, either
for efficiency or to provide access to operating system primitives such as
system calls.  The set of such modules is a configuration option which also
depends on the underlying platform For example, the :mod:`winreg` module is only
provided on Windows systems. One particular module deserves some attention:
:mod:`sys`, which is built into every Python interpreter.  The variables
``sys.ps1`` and ``sys.ps2`` define the strings used as primary and secondary
prompts::

   >>> import sys
   >>> sys.ps1
   '>>> '
   >>> sys.ps2
   '... '
   >>> sys.ps1 = 'C> '
   C> print 'Yuck!'
   Yuck!
   C>


These two variables are only defined if the interpreter is in interactive mode.

The variable ``sys.path`` is a list of strings that determines the interpreter's
search path for modules. It is initialized to a default path taken from the
environment variable :envvar:`PYTHONPATH`, or from a built-in default if
:envvar:`PYTHONPATH` is not set.  You can modify it using standard list
operations::

   >>> import sys
   >>> sys.path.append('/ufs/guido/lib/python')


.. _tut-dir:

The :func:`dir` Function
========================

:func:`dir` функцээр өгөгдсөн модул дотор ямар нэртэй тодорхойлолтууд
байна гэдгийг тодорхойлоход ашигладаг.Энэ нь эрэмблэгдсэн тэмдэгт төрлийн
жагсаалт буцаана::

   >>> import fibo, sys
   >>> dir(fibo)
   ['__name__', 'fib', 'fib2']
   >>> dir(sys)
   ['__displayhook__', '__doc__', '__excepthook__', '__name__', '__stderr__',
    '__stdin__', '__stdout__', '_getframe', 'api_version', 'argv',
    'builtin_module_names', 'byteorder', 'callstats', 'copyright',
    'displayhook', 'exc_clear', 'exc_info', 'exc_type', 'excepthook',
    'exec_prefix', 'executable', 'exit', 'getdefaultencoding', 'getdlopenflags',
    'getrecursionlimit', 'getrefcount', 'hexversion', 'maxint', 'maxunicode',
    'meta_path', 'modules', 'path', 'path_hooks', 'path_importer_cache',
    'platform', 'prefix', 'ps1', 'ps2', 'setcheckinterval', 'setdlopenflags',
    'setprofile', 'setrecursionlimit', 'settrace', 'stderr', 'stdin', 'stdout',
    'version', 'version_info', 'warnoptions']

Аргументтай :func:`dir` функц нь таны тодорхойлсон тодорхойлолтуудыг гаргадаг::

   >>> a = [1, 2, 3, 4, 5]
   >>> import fibo
   >>> fib = fibo.fib
   >>> dir()
   ['__builtins__', '__doc__', '__file__', '__name__', 'a', 'fib', 'fibo', 'sys']

Энд бүх төрлийн нэрүүдийн жагсаалт байна: хувьсагчууд, модулиуд, функцууд гэх мэт.

.. index:: module: __builtin__

:func:`dir` функц нь built-in функц болон хувьсагчийн нэрийн жагсаалтыг гаргадаггүй.
Хэрвээ энэ жагсаалтыг гаргаж авах бол  түүнийг стандарт модуль болох
:mod:`__builtin__` -ийг тодорхойлох хэрэгтэй::

   >>> import __builtin__
   >>> dir(__builtin__)
   ['ArithmeticError', 'AssertionError', 'AttributeError', 'DeprecationWarning',
    'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False',
    'FloatingPointError', 'FutureWarning', 'IOError', 'ImportError',
    'IndentationError', 'IndexError', 'KeyError', 'KeyboardInterrupt',
    'LookupError', 'MemoryError', 'NameError', 'None', 'NotImplemented',
    'NotImplementedError', 'OSError', 'OverflowError',
    'PendingDeprecationWarning', 'ReferenceError', 'RuntimeError',
    'RuntimeWarning', 'StandardError', 'StopIteration', 'SyntaxError',
    'SyntaxWarning', 'SystemError', 'SystemExit', 'TabError', 'True',
    'TypeError', 'UnboundLocalError', 'UnicodeDecodeError',
    'UnicodeEncodeError', 'UnicodeError', 'UnicodeTranslateError',
    'UserWarning', 'ValueError', 'Warning', 'WindowsError',
    'ZeroDivisionError', '_', '__debug__', '__doc__', '__import__',
    '__name__', 'abs', 'apply', 'basestring', 'bool', 'buffer',
    'callable', 'chr', 'classmethod', 'cmp', 'coerce', 'compile',
    'complex', 'copyright', 'credits', 'delattr', 'dict', 'dir', 'divmod',
    'enumerate', 'eval', 'execfile', 'exit', 'file', 'filter', 'float',
    'frozenset', 'getattr', 'globals', 'hasattr', 'hash', 'help', 'hex',
    'id', 'input', 'int', 'intern', 'isinstance', 'issubclass', 'iter',
    'len', 'license', 'list', 'locals', 'long', 'map', 'max', 'memoryview',
    'min', 'object', 'oct', 'open', 'ord', 'pow', 'property', 'quit', 'range',
    'raw_input', 'reduce', 'reload', 'repr', 'reversed', 'round', 'set',
    'setattr', 'slice', 'sorted', 'staticmethod', 'str', 'sum', 'super',
    'tuple', 'type', 'unichr', 'unicode', 'vars', 'xrange', 'zip']


.. _tut-packages:

Packages
========

Пакежууд бол Пайтонгийн модулийн нэрийн мужийг бүтэцлэх арга ба "цэгчилсэн модулийн 
нэр"-тэй.Жишээлбэл, :mod:`A.B` гэсэн модулийн нэр бол ``A`` гэсэн багцын
``B`` гэсэн дэд модуль байна. Just like the use of modules saves the
authors of different modules from having to worry about each other's global
variable names, the use of dotted module names saves the authors of multi-module
packages like NumPy or the Python Imaging Library from having to worry about
each other's module names.

Suppose you want to design a collection of modules (a "package") for the uniform
handling of sound files and sound data.  There are many different sound file
formats (usually recognized by their extension, for example: :file:`.wav`,
:file:`.aiff`, :file:`.au`), so you may need to create and maintain a growing
collection of modules for the conversion between the various file formats.
There are also many different operations you might want to perform on sound data
(such as mixing, adding echo, applying an equalizer function, creating an
artificial stereo effect), so in addition you will be writing a never-ending
stream of modules to perform these operations.  Here's a possible structure for
your package (expressed in terms of a hierarchical filesystem)::

   sound/                          Хамгийн дээд түвшний багч
         __init__.py               sound  багцийн байгуулагч
         formats/                  Файлын форматын дэд багч
                 __init__.py
                 wavread.py
                 wavwrite.py
                 aiffread.py
                 aiffwrite.py
                 auread.py
                 auwrite.py
                 ...
         effects/                  Дууны эффектийн дэд багц
                 __init__.py
                 echo.py
                 surround.py
                 reverse.py
                 ...
         filters/                  Шүүлтүүрүүдийн дэд багч
                 __init__.py
                 equalizer.py
                 vocoder.py
                 karaoke.py
                 ...

Багцыг импортлохдоо Пайтан ``sys.path`` ашиглан директоруудыг олон цааш нь
дэд директор луу ч нэвтрэн хайдаг.

The :file:`__init__.py` files are required to make Python treat the directories
as containing packages; this is done to prevent directories with a common name,
such as ``string``, from unintentionally hiding valid modules that occur later
on the module search path. In the simplest case, :file:`__init__.py` can just be
an empty file, but it can also execute initialization code for the package or
set the ``__all__`` variable, described later.

Users of the package can import individual modules from the package, for
example::

   import sound.effects.echo

Энэ нь :mod:`sound.effects.echo` дэд модулийг ачаална. Заахдаа бүтэн 
нэрээр нь дуудна. ::

   sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)

Дэд модулийг өөр аргаар импортлов::

   from sound.effects import echo

Энэ мөн л :mod:`echo` модулийг ачаалах бөгөөд, энд багцын препиксээр нь 
ачаалсан учир, дараах байдлаар хэрэглэж болно::

   echo.echofilter(input, output, delay=0.7, atten=4)

Өөр нэг зарлалт нь бол тухайн дуудах функц болон хувьсагчаа шууд импортлох юм::

   from sound.effects.echo import echofilter

Энэ нь мөн л  :mod:`echo` модулийг ачаалах бөгөөд, энд 
:func:`echofilter` гээд функцийн нэрийг шууд ашиглаж болно::

   echofilter(input, output, delay=0.7, atten=4)

Note that when using ``from package import item``, the item can be either a
submodule (or subpackage) of the package, or some  other name defined in the
package, like a function, class or variable.  The ``import`` statement first
tests whether the item is defined in the package; if not, it assumes it is a
module and attempts to load it.  If it fails to find it, an :exc:`ImportError`
exception is raised.

Contrarily, when using syntax like ``import item.subitem.subsubitem``, each item
except for the last must be a package; the last item can be a module or a
package but can't be a class or function or variable defined in the previous
item.


.. _tut-pkg-import-star:

Importing \* From a Package
---------------------------

.. index:: single: __all__

Now what happens when the user writes ``from sound.effects import *``?  Ideally,
one would hope that this somehow goes out to the filesystem, finds which
submodules are present in the package, and imports them all.  This could take a
long time and importing sub-modules might have unwanted side-effects that should
only happen when the sub-module is explicitly imported.

The only solution is for the package author to provide an explicit index of the
package.  The :keyword:`import` statement uses the following convention: if a package's
:file:`__init__.py` code defines a list named ``__all__``, it is taken to be the
list of module names that should be imported when ``from package import *`` is
encountered.  It is up to the package author to keep this list up-to-date when a
new version of the package is released.  Package authors may also decide not to
support it, if they don't see a use for importing \* from their package.  For
example, the file :file:`sounds/effects/__init__.py` could contain the following
code::

   __all__ = ["echo", "surround", "reverse"]

This would mean that ``from sound.effects import *`` would import the three
named submodules of the :mod:`sound` package.

If ``__all__`` is not defined, the statement ``from sound.effects import *``
does *not* import all submodules from the package :mod:`sound.effects` into the
current namespace; it only ensures that the package :mod:`sound.effects` has
been imported (possibly running any initialization code in :file:`__init__.py`)
and then imports whatever names are defined in the package.  This includes any
names defined (and submodules explicitly loaded) by :file:`__init__.py`.  It
also includes any submodules of the package that were explicitly loaded by
previous :keyword:`import` statements.  Consider this code::

   import sound.effects.echo
   import sound.effects.surround
   from sound.effects import *

In this example, the :mod:`echo` and :mod:`surround` modules are imported in the
current namespace because they are defined in the :mod:`sound.effects` package
when the ``from...import`` statement is executed.  (This also works when
``__all__`` is defined.)

Although certain modules are designed to export only names that follow certain
patterns when you use ``import *``, it is still considered bad practise in
production code.

Remember, there is nothing wrong with using ``from Package import
specific_submodule``!  In fact, this is the recommended notation unless the
importing module needs to use submodules with the same name from different
packages.


Intra-package References
------------------------

Дэд модулиуд нь ихэвчлэн бие биенээ заасан байдаг. Жишээ нь , 
:mod:`surround` модуль нь :mod:`echo` модулийг хэрэглэсэн
байж болно. Үнэн хэрэгтээ, эдгээр заалтууд дээр :keyword:`import` илэрхийлэл нь
стандарт модулийн хайх замаас хайхаас түрүүлэн багтаасан багцаас хайдаг.
Энэ :mod:`surround` модул нь  ``import echo`` эсвэл ``from echo import
echofilter`` хялбархан хэрэглэнэ. Хэрэв импортлосон модуль нь 
ажиллаж байгаа багцаас олдохгүй бол (багц нь ажиллаж байгаа модулийн дэд
модуль бол ),  :keyword:`import` илэрхийлэл өгсөн нэрний дээд түвшний
модулаас хайж эхэлдэг.

Багцууд нь дэд багцуудад бүтэцлэгдсэн үед (жишээн дээр :mod:`sound` багцыг
үзүүлсэн), та дэд модулиудын хооронд багцыг харьцангуйгаар импортлож болно.
Жишээлбэл, хэрэв модуль :mod:`sound.filters.vocoder`  :mod:`sound.effects` 
багцад байгаа :mod:`echo` модулийг ашиглах бол,дараах байдлаар бичиж болно ``from
sound.effects import echo``.

Starting with Python 2.5, in addition to the implicit relative imports described
above, you can write explicit relative imports with the ``from module import
name`` form of import statement. These explicit relative imports use leading
dots to indicate the current and parent packages involved in the relative
import. From the :mod:`surround` module for example, you might use::

   from . import echo
   from .. import formats
   from ..filters import equalizer

Note that both explicit and implicit relative imports are based on the name of
the current module. Since the name of the main module is always ``"__main__"``,
modules intended for use as the main module of a Python application should
always use absolute imports.


Packages in Multiple Directories
--------------------------------

Багцууд нь бас нэг тусгай аттрибутыг дэмждэг, :attr:`__path__`. Энэ нь 
директорын нэрийг жагсаалтыг агуулж байгаа тухайн багцын :file:`__init__.py` 
файл доторх код ажиллахаас өмнө анхны утга олгогдсон байдаг.Энэ хувьсагчийн
утга нь тухайн багцад байгаа модулиудыг хайхад өөрчлөгдсөн байдаг .

While this feature is not often needed, it can be used to extend the set of
modules found in a package.


.. rubric:: Footnotes

.. [#] In fact function definitions are also 'statements' that are 'executed'; the
   execution of a module-level function enters the function name in the module's
   global symbol table.

