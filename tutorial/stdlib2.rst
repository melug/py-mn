.. _tut-brieftourtwo:

**********************************************
Стандарт сангуудаар аялах товч аялал 2-р хэсэг
**********************************************

Энэхүү хоёрдахь аялалаараа мэргэжлийн програмчлалын хэрэгцээг хангасан
илүү ахисан түвшний модулиудыг танилцуулах болно. Эдгээр модуль ховорхон
тохиолдох жижиг скритүүд юм.


.. _tut-output-formatting:

Гаралтын хэвжүүлэлт
===================

:mod:`repr` модуль нь :func:`repr` функцийн сайжруулсан хувилбар бөгөөд 
том хэмжээний дэлгэц эсвэл гүнд задарсан агуулахыг багасгах зорилготой
юм::

   >>> import repr
   >>> repr.repr(set('supercalifragilisticexpialidocious'))
   "set(['a', 'c', 'd', 'e', 'f', 'g', ...])"

:mod:`pprint` модуль нь байгуулагдсан болон хэрэглэгчийн тодорхойлсон объектыг
интерпретер дээр илүү ойлгомжтой үзүүлэхэд өндөр мэдрэмжтэй удирддаг.
Үр дүн нь нэг мөрөөс илүү их болох үед, "сайн принтер нь" өгөгдлийн бүтцийг
илрүүлэн зэрэгцүүлэлт хийх болон таслах мөр нэмдэг::

   >>> import pprint
   >>> t = [[[['black', 'cyan'], 'white', ['green', 'red']], [['magenta',
   ...     'yellow'], 'blue']]]
   ...
   >>> pprint.pprint(t, width=30)
   [[[['black', 'cyan'],
      'white',
      ['green', 'red']],
     [['magenta', 'yellow'],
      'blue']]]

:mod:`textwrap` модуль нь параграф текстийг өгөгдсөн дэлгэцийн өргөнд тааруулж
хэвжүүлдэг::

   >>> import textwrap
   >>> doc = """The wrap() method is just like fill() except that it returns
   ... a list of strings instead of one big string with newlines to separate
   ... the wrapped lines."""
   ...
   >>> print textwrap.fill(doc, width=40)
   The wrap() method is just like fill()
   except that it returns a list of strings
   instead of one big string with newlines
   to separate the wrapped lines.

:mod:`locale` модуль соёл боловсролын тусгай өгөгдлийн форматын өгөгдлийн сан
руу ханддаг.
Локалийн формат функцийн аттрибутийг бүлэглэн хэвжүүлэлтийн дугаараар шууд
хандах боломж олгодог::

   >>> import locale
   >>> locale.setlocale(locale.LC_ALL, 'English_United States.1252')
   'English_United States.1252'
   >>> conv = locale.localeconv()          # get a mapping of conventions
   >>> x = 1234567.8
   >>> locale.format("%d", x, grouping=True)
   '1,234,567'
   >>> locale.format_string("%s%.*f", (conv['currency_symbol'],
   ...                      conv['frac_digits'], x), grouping=True)
   '$1,234,567.80'


.. _tut-templating:

Templating
==========

:mod:`string` модуль нь төрөл бүрийн :class:`Template` классд багтдаг бөгөөд
эцсийн хэрэглэгчээр засуулахад зориулан бичиглэлийг хялбарчилдаг. Ингэснээр
хэрэглэгч нь өөрийн програмаа өөр програмтай нэгтгэн сайжруулахад тус болно.

Формат нь байралын нэр ашиглахдаа Пайтонд таниулахын тулд ``$`` тэмдэг
ашигладаг байна.(альфа тооны тэмдэгтүүд болон доогуур зураас) Байрлалын
нэрээ угалзан хаалтаар хаах бөгөөд араас нь тэмдэгтүүд завсрын зайгүй 
хэрэглэж болно. ``$`` бичихдээ ``$$`` бичнэ:: 

   >>> from string import Template
   >>> t = Template('${village}folk send $$10 to $cause.')
   >>> t.substitute(village='Nottingham', cause='the ditch fund')
   'Nottinghamfolk send $10 to the ditch fund.'

:meth:`substitue` метод нь толь эсвэл гарнаас өгсөн аргументад байрлалын нэр
өгөгдөөгүй бол :exc:`KeyError` алдаа өгдөг. Майл нийлүүлэх стилийн програмд 
хэрэглэгч өгөгдлөө бүрэн бус өгж болох ба :meth:`safe_substitute` метод нь
энэ тохиолдолд магадгүй илүү тохиромжтой байж болно--- хэрэв өгөгдөл өгөгдөөгүй
бол өөрчлөгдөөгүй нэрийг орхиод явна::

   >>> t = Template('Return the $item to $owner.')
   >>> d = dict(item='unladen swallow')
   >>> t.substitute(d)
   Traceback (most recent call last):
     . . .
   KeyError: 'owner'
   >>> t.safe_substitute(d)
   'Return the unladen swallow to $owner.'

Загвар дэд класс нь тусгайлан хувийн өгөгдлийн хязгаарлагч болж чадна.
Жишээлбэл, фото хөтөчид зориулсан нэрлэх багаж хэрэгсэл нь одоогийн он
сар, зургийн давтамжийн дугаар, эсвэл файлын формат гэх мэт байрлалын
нэрүүдэд хувийн тэмдэг ашиглахаар сонгож болно::

   >>> import time, os.path
   >>> photofiles = ['img_1074.jpg', 'img_1076.jpg', 'img_1077.jpg']
   >>> class BatchRename(Template):
   ...     delimiter = '%'
   >>> fmt = raw_input('Enter rename style (%d-date %n-seqnum %f-format):  ')
   Enter rename style (%d-date %n-seqnum %f-format):  Ashley_%n%f

   >>> t = BatchRename(fmt)
   >>> date = time.strftime('%d%b%y')
   >>> for i, filename in enumerate(photofiles):
   ...     base, ext = os.path.splitext(filename)
   ...     newname = t.substitute(d=date, n=i, f=ext)
   ...     print '{0} --> {1}'.format(filename, newname)

   img_1074.jpg --> Ashley_0.jpg
   img_1076.jpg --> Ashley_1.jpg
   img_1077.jpg --> Ashley_2.jpg

Загварт зориулсан өөр програмд програмын логикыг олон гаралтын форматын 
дэлгэрэнгүйгээс салгахын тулд хэрэглэдэг. Энэ нь хувийн загварт тохирсон 
XML файлууд, энгийн текст тайлангууд, HTML веб тайлангуудыг үүсгэх 
боломжтой гэсэн үг. 


.. _tut-binary-formats:

Бинари өгөгдөлтэй ажиллах
=========================

:mod:`struct` модул нь хувьсах урттай бинари форматтай ажиллах :func:`pack` болон
:func:`unpack` гэсэн функцүүдтэй. Дараах жишээн дээр ZIP файлын толгойн хэсгийн
мэдээлэлд давталт хийн жишээг :mod:`zipfile` модулийн тусламжтайгаар харуулсан 
байна. Багц ``"H"`` болон ``"I"`` кодууд нь нэрлэсэн дарааллаар хоёр болон дөрвөн
тэмдэггүй тоог үзүүлнэ. ``"<"`` энэ нь стандарт хэмжээ болон бага эндиан байтын
дарааллыг илэрхийлдэг::

   import struct

   data = open('myfile.zip', 'rb').read()
   start = 0
   for i in range(3):                      # show the first 3 file headers
       start += 14
       fields = struct.unpack('<IIIHH', data[start:start+16])
       crc32, comp_size, uncomp_size, filenamesize, extra_size = fields

       start += 16
       filename = data[start:start+filenamesize]
       start += filenamesize
       extra = data[start:start+extra_size]
       print filename, hex(crc32), comp_size, uncomp_size

       start += extra_size + comp_size     # skip to the next header


.. _tut-multi-threading:

Multi-threading
===============

Threading бол дараалсан хамааралгүйгээр хосоор ажиллуулах текник юм.
Threads програмын мэдрэмжийг нэмэгдүүлэх бөгөөд хэрэглэгч гараас утга
хүлээж байх хооронд арын процесст өөр ажил ажиллаж байх юм. Хоорондоо
хамааралтай оролт гаралын паралелаар ажиллаж байгаа тохиолдолд тооцооллын
өөр трэдтэй байдаг. 

Дараах код нь дээд түвшний :mod:`threading` үндсэн модуль үргэлжлэн ажиллаж
байхад ард нь хэрхэн ажиллаж чаддагыг харуулна::

   import threading, zipfile

   class AsyncZip(threading.Thread):
       def __init__(self, infile, outfile):
           threading.Thread.__init__(self)
           self.infile = infile
           self.outfile = outfile
       def run(self):
           f = zipfile.ZipFile(self.outfile, 'w', zipfile.ZIP_DEFLATED)
           f.write(self.infile)
           f.close()
           print 'Finished background zip of: ', self.infile

   background = AsyncZip('mydata.txt', 'myarchive.zip')
   background.start()
   print 'The main program continues to run in foreground.'

   background.join()    # Wait for the background task to finish
   print 'Main program waited until background was done.'

Олон трэдтэй програмын хамгийн чухал шаардлага бол хуваасан өгөгдөл эсвэл 
бусад нөөцийг харилцан уялдуулахад оршино. Энэ хүртэл, threading модуль нь 
олон тооны цоож агуулсан үндсэн синхрон, эвентүүд, нөхцөлт хувьсагчууд, 
болон семафоруудыг олгодог.

Тэдгээр хэрэгслүүд хүчирхэг байхад, бага зэргийн дизайны алдаанууд өөрөөр 
хуулбарлан бүтээхэд асуудал үүсгэж чадна. Ийм учраас, онцгой эрхтэй дөхөлт нь
ажил хуваарилалт хийхдээ нэг трэдээс бүх нөөц рүү хандах ба :mod:`Queue` модуль 
нь бусад трэдээс шаардлагатай мэдээллээр хангахад тусладаг. Програмд хэрэглэхдээ
:class:`Queue.Queue` объектийг трэд хоорондын холбоо болон зохицуулахад илүү 
хялбар, илүү эвтэйхэн, илүү уян хатан загварчлагдсан.


.. _tut-logging:

Logging
=======

:mod:`logging` модуль нь бүрэн засагдсан уян хатан логийн систем юм.
Хамгийн энгийнээр лог бичлэгийг файл эсвэл стандарт алдаа ``sys.stderr``
руу гаргаж болно::

   import logging
   logging.debug('Debugging information')
   logging.info('Informational message')
   logging.warning('Warning:config file %s not found', 'server.conf')
   logging.error('Error occurred')
   logging.critical('Critical error -- shutting down')

Энэ нь дараах гаралтыг гаргана::

   WARNING:root:Warning:config file server.conf not found
   ERROR:root:Error occurred
   CRITICAL:root:Critical error -- shutting down

Анхны утгаараа мэдээллийн болон дебугийн мессежийн гаралтыг стандарт алдаа 
руу илгээдэг. Бусад гаралтын сонголтууд нь чиглүүлэх мессежэд багтдаг ба үүнд
майл явуулах, датаграмууд, сокетууд, эсвэл HTTP сервер байж болно. Шинэ 
шүүлтүүрүүд нь мессежний зэрэглэлээр чиглүүлэгддэг: :const:`DEBUG`, 
:const:`INFO`,:const:`WARNING`, :const:`ERROR`, and :const:`CRITICAL`.

Лог бичлэгийн систем нь Пайтонгоос шууд тохируулагддаг эсвэл хэрэглэгч өөрчлөх
боломжтой тохиргооны файл өөрсдөө зохион бичиж болно.


.. _tut-weak-references:

Нэр хүндгүй заалтууд
====================

Пайтон автомат санах ойн удирдлагатай(ихэнх объектуудын заалтыг тоолох болон
:term:`garbage collection` -р циклийг тогтоодог). Санах ой бол сүүлийн заалт
чөлөөлөгдсний дараа чөлөөлөгддөг.

Энэ нь ихэнх програм дээр сайн ажилладаг боловч санамсаргүй тохиолдолд 
объектийг олохдоо болон зарим нэг юманд ашиглаж болно. Харамсалтай нь 
ингэж мөшгөхөд түүний заалтыг үүсгэдэг түүнийг тэр чигээр нь үлдээдэг.
:mod:`weakref` модуль нь объектыг түүний заалттай нь үүсгэх хэрэгслээр 
хангадаг. Объект нь түр хугацаанл хэрэгтэй үед сул заалтын хүснэгтээс
хасагдах ба сул заалтын объектуудад зориулан эргэн дуудагддаг. Энгийн 
програмууд нь объектыг кэшлэдэг бөгөөд тэр нь үүсгэхэд хэтэрхий 
үрэлгэн болдог::

   >>> import weakref, gc
   >>> class A:
   ...     def __init__(self, value):
   ...             self.value = value
   ...     def __repr__(self):
   ...             return str(self.value)
   ...
   >>> a = A(10)                   # create a reference
   >>> d = weakref.WeakValueDictionary()
   >>> d['primary'] = a            # does not create a reference
   >>> d['primary']                # fetch the object if it is still alive
   10
   >>> del a                       # remove the one reference
   >>> gc.collect()                # run garbage collection right away
   0
   >>> d['primary']                # entry was automatically removed
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
       d['primary']                # entry was automatically removed
     File "C:/python26/lib/weakref.py", line 46, in __getitem__
       o = self.data[key]()
   KeyError: 'primary'


.. _tut-list-tools:

Жагсаалттай ажиллах хэрэгслүүд
==============================

Олон өгөгдлийн бүтэц дээр бид жагсаалт төрөлтэй таардаг. Харин,
зарим тохиолдолд үүнийг хийхэд арай өөр хэрэгжүүлэлт хэрэг болдог.

:mod:`array` модуль нь :class:`array()` объект үүсгэдэг бөгөөд энэ нь 
яг л жагсаалт шиг зөвхөн нэг төрлийн өгөгдөл хадгалдаг бас их нягт байдаг.
Дараах жишээ код нь хоёр байтын тэмдэггүй хоёртын тоо байдлаар жагсаалт 
болгон (төрлийн код ``"H"``)  хадгалаад энгийн 16 байт Пайтонгийн инт объект 
болгон ашиглаж байна::

   >>> from array import array
   >>> a = array('H', [4000, 10, 700, 22222])
   >>> sum(a)
   26932
   >>> a[1:3]
   array('H', [10, 700])

:mod:`collections` модуль нь :class:`deque()` классын объект бөгөөд жагсаалтад
зүүн талаас нь нэмэх болон гаргадаг учир маш хурдан гэхдээ хайхад удаан байдаг.
Эдгээр объектууд н дараалал(queue) болон өргөнөөр хайх модны хайлтыг 
хэрэгжүүлэхэд яг таардаг::

   >>> from collections import deque
   >>> d = deque(["task1", "task2", "task3"])
   >>> d.append("task4")
   >>> print "Handling", d.popleft()
   Handling task1

   unsearched = deque([starting_node])
   def breadth_first_search(unsearched):
       node = unsearched.popleft()
       for m in gen_moves(node):
           if is_goal(m):
               return m
           unsearched.append(m)

Нэмх хэлэхэд өөр жагсаалтын хэрэгжүүлэлтүүд нь сангийн бусад хэрэгслүүдэд 
санал болгодог бөгөөд тэдний нэг :mod:`bisect` модуль нь функцуудийнхээ
хамт эрэмблэгдсэн жагсаалтыг удирдахад дөхөм болдог байна.::

   >>> import bisect
   >>> scores = [(100, 'perl'), (200, 'tcl'), (400, 'lua'), (500, 'python')]
   >>> bisect.insort(scores, (300, 'ruby'))
   >>> scores
   [(100, 'perl'), (200, 'tcl'), (300, 'ruby'), (400, 'lua'), (500, 'python')]

:mod:`heapq` модульийн функцууд нь энгийн жагсаалт дээр овоолго(heap)-ийг 
хэрэгжүүлэх боломжийг олгодог. Хамгийн үр ашиггүй орсон утга нь үргэлж
тэг байрлалаа хадгалдаг. Үүнийг програмд хэрэглэхэд амар бөгөөд хамгийн 
бага элемент рүү нь шууд ханддаг гэхдээ үүнийг жагсаалтыг эрэмблэхэд 
хэрэглэх нь тийм ч сайхан санаа биш::

   >>> from heapq import heapify, heappop, heappush
   >>> data = [1, 3, 5, 7, 9, 2, 4, 6, 8, 0]
   >>> heapify(data)                      # rearrange the list into heap order
   >>> heappush(data, -5)                 # add a new entry
   >>> [heappop(data) for i in range(3)]  # fetch the three smallest entries
   [-5, 0, 1]


.. _tut-decimal-fp:

Бутархай хөвөгч тооны арифметик
===============================

:mod:`decimal` модуль нь :class:`Decimal` гэсэн классыг бутархай хөвөгч 
арифметик тооны өгөгдлийн төрлийг дүрслэхэд санал болгодог. Хоёртын хөвөгч
тоог хэрэгжүүлэх :class:`float` классыг харьцуулсан ба энэ класс нь тусгайлан
танд дараах зүйлийг хийхэд туслана

* санхүүгийн програм болон бусад хэрэглээнд бутархай тоог яг нарийвлалтайгаар
  үзүүлэх
* нарийвчлалийг удирдах 
* албан ёсны эсвэл захиргааны шаардлагаар шатлалыг удирдах
* ач холбогдолтой бутархай хэсгийг ажиглах эсвэл
* хэрэглэгч тооцооллын үр дүнг програмаас хүсэх

Жишээлбэл, утас цэнэглэсний хөлс 70 центээ татвар нь 5 хувийг бодохдоо 
бутархай хөвөгч тоо болон хоёртын хөвөгч тооноос ялгаатай үр дүн гарна. 
Энэ ялгаа нь хэрэв үр дүнг ойролцоо цент руу дугуйлсан бол гарна::

   >>> from decimal import *
   >>> x = Decimal('0.70') * Decimal('1.05')
   >>> x
   Decimal('0.7350')
   >>> x.quantize(Decimal('0.01'))  # round to nearest cent
   Decimal('0.74')
   >>> round(.70 * 1.05, 2)         # same calculation with floats
   0.73

:class:`Decimal` класс нь үр дүнд тэгийг хадгалдаг, автоматаар хоёр оронтой
хэмжээний үржигдэхүүн дөрвөн хэмжээг боддог. Бутархай нь танд математикийг 
сэргээх ба хоёртын хөвөгч тоо нь бутархайн чанарыг яг нарийн үзүүлж чадахгүй
үед энэ асуудлыг шийдэж өгөх болно.

Нарийвчлалтай үзүүлэхдээ :class:`Decimal` классыг өөрийн тооцооллын модульдаа
хэрэгжүүлэх ба хоёртын хөвөгч тоонд тохиронхгүй гэдгийг шалгаж болно::

   >>> Decimal('1.00') % Decimal('.10')
   Decimal('0.00')
   >>> 1.00 % 0.10
   0.09999999999999995

   >>> sum([Decimal('0.1')]*10) == Decimal('1.0')
   True
   >>> sum([0.1]*10) == 1.0
   False

:mod:`decimal` модуль арифметикийн яг нарийвчилсан хариуг гаргахад хэрэг болдог::

   >>> getcontext().prec = 36
   >>> Decimal(1) / Decimal(7)
   Decimal('0.142857142857142857142857142857142857')


