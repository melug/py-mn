.. _tut-modules:

********
Модулиуд
********

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

   #Фибаночийн тооний модуль

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

Модулийн дэлгэрэнгүй
====================

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

Модулийг скрипт шиг ажиллуулах
------------------------------

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

Модулийн хайх зам
-----------------

.. index:: triple: module; search; path

:mod:`spam` нэртэй модуль импортлоход, интерпретер нь :file:`spam.py` нэртэй 
файлыг тухайн директороос хайдаг мөн түүнчлэн :envvar:`PYTHONPATH` орчны 
хувьчагчид заасан толины жагсаалтаас ч бас асуудаг. Энэ орчны хувьсагч нь 
:envvar:`PATH` хувьсагчтай адилхан синтакстай бөгөөд директорын нэрийн 
жагсаалт байна. :envvar:`PYTHONPATH` орчны хувьсагчийг тодорхойлоогүй үед, 
эсвэл файл олдоогүй үед хайлтыг үргэлжлүүлэн суулгах анхны зам болох 
:file:`.:/usr/local/lib/python` (Unix дээр ихэвчлэн ийм байдаг) -ээс
хайдаг.

Үнэн хэрэгтээ, модулиудыг директорын жагсаалтыг бидэнд өгөх оролтын 
скриптээс утга олгогдсон ``sys.path`` хувьсагчаас(эсвэл ажиллаж байгаа директор),
:envvar:`PYTHONPATH` болон суулгацын анхны замаас хайдаг байна. Энэ нь Пайтон 
програмд модулийн хайх замыг өөрчлөх болон солихыг зөвшөөрдөг.Гэхдээ та эдгээр 
хайх замууд дотор болон стандарт модультай адилхан нэртэй файл бичиж болохгүйг 
анхаарах хэрэгтэй эсвэл Пайтон нь скриптыг ачаалах оролдлого хийхэд аль хэдийн
импортлосон байх юм. Энэ тохиолдолд ерөнхийдөө алдаа өгнө. Илүү дэлгэрэнгүй
мэдээллийг :ref:`tut-standardmodules` -аас үзнэ үү.


"Хөрвүүлэгдсэн" Пайтон файлууд
------------------------------

Стандарт модулийг ихэвчлэн хэрэглэдэг жижиг хэмжээний програмуудын хувьд
програм эхлэх цагыг илүү хурдан болгохын тулд :file:`spam.py` файлын 
директор дотор :file:`spam.pyc` нэртэй файл байх бөгөөд энэ нь :mod:`spam`
модулийн "байт руу хөрвүүлэгдсэн" хувилбар юм. :file:`spam.py` файлын
засварлалт бүрд :file:`spam.pyc` файлыг үүсгэх ба өөрчлөлт болгон нь бичигдэж
байдаг бөгөөд өмнөх хөрвүүлэгдсэн файлтай ижилхэн байвал :file:`.pyc` юу ч 
өөрчлөхгүй. 

Энгийнээр хэлбэл, :file:`spam.pyc` файлыг үүсгэх гэж юу ч хийх хэрэггүй.
Хэдийд ч хамаагүй :file:`spam.py` файл амжилттай хөрвүүлэгдэх үед хөрвүүлэгдсэн
:file:`spam.pyc` файл руу бичих оролдлого хийдэг. Оролдлого нь амжилтгүй болвол
энэ нь алдаа гарсан гэсэн үг; эсвэл ямар нэг шалтгаанаар файл гүйцэд бичилт 
хийж чадаагүй байж болно, энэ тохиолдолд :file:`spam.pyc` файл нь танигдахгүй.
:file:`spam.pyc` файлын агуулга нь платформ хамааралгүй, тэгэхээр Пайтонгийн
модуль нь өөр архитектурын машин дээр хуваагдсан байж болно.


Экспертүүдэд хэдэн зөвлөмж:

* Пайтон интерпретерийг -O сонголттой дуудсан тохиолдолд сайжруулагдсан код нь
  үүсгэгдэн :file:`.pyo` файлуудад хадгалагддаг. Энэ сайжруулагч нь нэг их тус
  хүргэхгүй, зөвхөн :keyword:`assert` илэрхийллүүдийг л хасдаг. :option:`-O`
  сонголтыг хэрэглэх үед *бүх* :term:`bytecode` нь сайжруулагдана; ``.pyc``
  файлуудыг нь алгасан ``.py`` файлууд нь сайжруулагдсан байткод руу хөрүүлэгддэг.

* 2 ширхэг :option:`-O` флагтай Пайтон интерпретер нь(:option:`-OO`)  байт код
  хөрвүүлэгчид зарим жижиг програмын хааяа л хэрэглэдэг үр дүнгүүдийг хасахаар
  зааж өгдөг. Одоогоор байт кодоос ``__doc__`` тэмдэгтүүдийг хасдаг ба үр дүнд
  нь илүү авсаархан :file:`.pyo` файлуудыг гаргадаг. Зарим програмд эдгээр 
  зүйлсийг хэрэглэх нь зөв гэж үзсэн бол энэхүү сонголтыг хэрэглэх нь тохиромжтой
  юм.

* Програм нь :file:`.pyc` эсвэл :file:`.pyo` файл нь :file:`.py` файлаасаа уншин
  ажилахдаа хурдан ажилладаггүй; :file:`.pyc` эсвэл :file:`.pyo` файлууд нь 
  ачаалагдсан бол хурдан ажилладаг.

* Скриптийг командын мөрөөс нэрийг нь өгөн ажиллуулах үед, байткодод зориулсан
  :file:`.pyc` эсвэл :file:`.pyo` файл руу хэзээ ч бичилт хийдэггүй. Тиймээс
  модулийн кодыг зөөх болон жижиг эхлүүлэгч програм руу модулийг импортлох 
  скриптийн эхлэх хугацааг багасгадаг.Ингэснээр та командын мөрөөс шууд
  :file:`.pyc` эсвэл :file:`.pyo` шууд ашиглаж болно. 

* :file:`spam.pyc` нэртэй файл нь (эсвэл :option:`-O` сонголт 
  хэрэглэсэн үед :file:`spam.pyo` ) :file:`spam.py` файлтай ижил модуль байна.
  Энэ нь таны Пайтон кодыг тараахад хэрэг болох ба реверс енжинээр хийхэд
  хэцүү болно.

  .. index:: module: compileall

* :mod:`compileall` модуль нь :file:`.pyc` файлуудыг  (эсвэл :option:`-O` 
  сонголт хэрэглэсэн үед :file:`spam.pyo` ) бүх модулийн директорт үүсгэдэг.


.. _tut-standardmodules:

Стандарт модулиуд
=================

.. index:: module: sys

Пайтон нь стандарт модулиудын сангуудтай бөгөөд түүнийг Python Library 
Reference("Library Reference" дараа үзнэ ) баримтжуулалт болгон салгасан.
Зарим модулиуд нь интерпретерт суурилсан байдаг;
document, the Python Library Reference ("Library Reference" hereafter). 
Зарим модулиуд нь гүйцэтгэгчийг байгуулдаг бөгөөд эдгээр нь хэлний гол
хэсгээр хандаж чаддаггүй гэвч эдгээр нь байгуулж чаддаг доорх хоёрыг 
үр дүн болон үйлдлийн системд хандах эрхээр хангадаг системийн дуудалт юм.
system calls. Цогц модулиуд бол тохиргооны сонголт бөгөөд тэр нь платформын
үндсэнд байдаг. Жишээлбэл, :mod:`winreg` модуль нь зөвхөн Windows системд 
байдаг. Нэг тодорхой модульд зарим анхаарал хандуул:
:mod:`sys`, Пайтон интерпретер бүр дээр суурилсан. ``sys.ps1`` ба ``sys.ps2``
хувьсагчууд нь тэмдэгтүүдийг анхдагч болон хоёрдогч prompt болгон тодорхойлоход
хэрэглэдэг::

   >>> import sys
   >>> sys.ps1
   '>>> '
   >>> sys.ps2
   '... '
   >>> sys.ps1 = 'C> '
   C> print 'Yuck!'
   Yuck!
   C>


Эдгээр хоёр хувьсагчууд нь зөвхөн интерпретерийн харилцах горимд тодорхойлогдсон.

``sys.path`` хувьсагч бол тэмдэгтийн жагсаалт байх ба энэ нь интерпретерийн 
модулын зам хайхад хэрэглэгдэнэ. Анхны зам нь :envvar:`PYTHONPATH` орчны 
хувьсагчаас утга нь олгогдсон байдаг, эсвэл :envvar:`PYTHONPATH` тохируулаагүй
бол ажилласан замаа авдаг. Та энэ стандарт жагсаалтыг засахдаа дараах үйлдлийг 
хийнэ::

   >>> import sys
   >>> sys.path.append('/ufs/guido/lib/python')


.. _tut-dir:

:func:`dir` функц
=================

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

Багцууд
=======

Пакежууд бол Пайтонгийн модулийн нэрийн мужийг бүтэцлэх арга ба "цэгчилсэн модулийн 
нэр"-тэй.Жишээлбэл, :mod:`A.B` гэсэн модулийн нэр бол ``A`` гэсэн багцын
``B`` гэсэн дэд модуль байна. Яг үүнтэй адилхан зохиогч нь хувьсагч хэрэглэхдээ
өөр модулийн хувьсагчаас ялгаатай нэрлэх гэж санаа зовсны хэрэггүй, цэгтэй нэр 
хэрэглэн Numpy эсвэл Python Зургийн сан шиг олон модуль болгон салгаж модуль доторх 
зүйлүүд бусад модулиас хамааралгүй болно.

Дууны файл, дууны өгөгдлийн нэгэн хэвийн загварт зориулсан модулийн цуглуулга 
бичих гэж үзье. Тэнд маш олон ялгаатай дууны файлын форматууд(ихэвчлэн танихдаа
файлынх нь өргөтгөлөөр нь таньдаг, жишээлбэл: :file:`.wav`,:file:`.aiff`, 
:file:`.au`), тэгэхээр чи ялгаатай файлын форматуудын хоорондох холбоог үүсгэхийн
тулд магадгүй модулийн багц үүсгэх хэрэгтэй. Тэдгээр маш олон ялгаатай үйлдлүүд 
байх ба магадгүй чи дууны өгөгдлийг хэлбэржүүлэхийг хүсэж болох юм(холих, 
цуурай нэмэх,тэнцвэржүүлэгч хэрэглэх, стерео эффект нэмэ ), ингээд чи нэмж хэзээ
ч төгсөшгүй модулийн урсгалыг бичин эдгээр үйлдлийг хийж болно. Дараах бүтцээр
үүнийг хийж болно(файлын системийн шатлалыг томъёолов)::

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

:file:`__init__.py` файлууд нь директорийг Пайтон багц болгоход шаардлагатай;
энэ нь директорыг нийтлэг нэр болгон анхааруулна, яг л ``string`` шиг, 
санамсаргүйгээр зөв модулийг хайх замд нуух тохиолдол байдаг. Хамгийн энгийн
тохиолдолд, :file:`__init__.py`  файл нь хоосон  файл байж болно, гэвч утга 
багцад зориулсан эсвэл ``__бүх__`` хувьсагчийн утга олгох үйлдлийг энэ файлд
бичин ажиллуулж болно.

Хэрэглэгчийн өөрийн хувийн модулийг багцаас импортлож болно жишээлбэл::

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


``from package import item`` ингэж ашиглаж байгаа үед, item нь багцын дэд модуль
(эсвэл дэд багч), эсвэл багцад тодорхойлогдсон функц, класс, хувьсагч байж болно 
гэдгийг анхаарах хэрэгтэй. ``import`` илэрхийлэл нь item багцад тодорхойлогдсон
эсвэл тодорхойлогдоогүй байсан ч ялгаагүй хамгийн эхэнд модулийг импортлох
оролдлого хийдэг. Хэрэв хайлт амжилтгүй болвол :exc:`ImportError` алдаа үзүүлдэг.

Эсрэгээр ``import item.subitem.subsubitem`` синтакс хэрэглэж байгаа бол , item бүр 
нь багцыг үл тооцон хамгийн сүүд байна; сүүлийн item модуль эсвэл багц байж
чадна гэхдээ класс эсвэл функц эсвэл өмнө тодорхойлсон хувьсагч байж болохгүй.

.. _tut-pkg-import-star:

Багцаас *-оор импортлох
-----------------------

.. index:: single: __all__

Хэрэглэгч ``from sound.effects import *`` ингэж бичвэл юу болох вэ? Онолын үүднээс,

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


Дотоод багцын заалтууд
----------------------

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


Олон директор дахь багцууд
--------------------------

Багцууд нь бас нэг тусгай аттрибутыг дэмждэг, :attr:`__path__`. Энэ нь 
директорын нэрийг жагсаалтыг агуулж байгаа тухайн багцын :file:`__init__.py` 
файл доторх код ажиллахаас өмнө анхны утга олгогдсон байдаг.Энэ хувьсагчийн
утга нь тухайн багцад байгаа модулиудыг хайхад өөрчлөгдсөн байдаг .

Хэдийгээр энэ боломж нь тэгтлээ өргөн хэрэглэгддэггүй ч гэсэн үүнийг 
багц дахь модулиудыг өргөтгөх замаар хэрэглэж болно.


.. rubric:: Footnotes

.. [#] In fact function definitions are also 'statements' that are 'executed'; the
   execution of a module-level function enters the function name in the module's
   global symbol table.

