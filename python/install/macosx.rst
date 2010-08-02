Мак ОС Икс дээр
###############

Нэгэнт л Пайтон суулгах талаар өгүүлж байгаа болохоор Мак ОС Иксийг нүд үзүүрлээд яахав, тийм ээ?

Мак ОС Икс дээр Пайтонг суулгах хоёр арга бий: нэг нь суулгах, нөгөө нь суулгахгүй байх.

Мак ОС Икс 10.2 хувилбараас эхлэн Пайтоны бүрхүүлийн хувилбартай ирдэг болсон.

Суугдан ирсэн Пайтонг ажиллуулах нь
-----------------------------------

#. ``/Applications`` хавтасыг нээ.
#. ``Utilities`` хавтасыг нээ.
#. ``Terminal`` дээр хоёр дараад бүрхүүлийг ажиллуул.
#. ``Тушаалын мөр`` дээр ``python`` гэж бичээд Enter дар.

Нэг иймэрхүү юм харагдах байх:

::

    Welcome to Darwin!
    [localhost:~] you% python
    Python 2.2 (#1, 07/14/02, 23:25:09)
    [GCC Apple cpp-precomp 6.14] on darwin
    Type "help", "copyright", "credits", or "license" for more information.
    >>> [press Ctrl+D to get back to the command prompt]
    [localhost:~] you% 

Пайтоны хамгийн сүүлийн хувилбарыг суулгах нь
---------------------------------------------

#. http://homepages.cwi.nl/~jack/macpython/download.html хаягаас ``MacPython-OSX`` хэмээх хуурцагны дүрс файлыг татчих.
#. ``MacPython-OSX-2.3-1.dmg`` дүрс файл дээрээ хоёр дараад залгачих.
#. ``MacPython-OSX.pkg`` суулгагч дээр хоёр дараад эхлүүл.
#. Суулгагч чиний удирдлагын нэр, нууц үгийг асуухаар бичээд өгчихөөрэй.
#. Суулгаж дуусаад ``/Applications`` хавтасыг нээ.
#. ``MacPython-2.3`` хавтасыг нээ.
#. ``PythonIDE`` дээр хоёр дараад Пайтонг ажиллуул.

Ингэхэд МакПайтон IDE эхлэлийн дэлгэц харуулаад интерактив бүрхүүл нээнэ. Хэрвээ бүрхүүл харагдахгүй бол ``Window->Python Interactive **(Cmd-o)**`` гэж сонгоорой. Нээгдэх цонхонд дараах мэдээлэл харагдах байх:

::

    Python 2.3 (#2, Jul 30 2003, 11:45:28)
    [GCC 3.1 20020420 (prerelease)]
    Type "copyright", "credits" or "license" for more information.
    MacPython IDE 1.0.1
    >>> 

Хэдийгээр хамгийн сүүлийн хувилбарыг суулгасан ч нөгөө хуучин хувилбар чинь байж л байгаа. Тушаалын мөрөөс скрипт ажиллуулахдаа алийг нь хэрэглэж байгаагаа анзаараарай.

**Пайтоны хоёр хувилбар**::

 [localhost:~] you% python
 Python 2.2 (#1, 07/14/02, 23:25:09)
 [GCC Apple cpp-precomp 6.14] on darwin
 Type "help", "copyright", "credits", or "license" for more information.
 >>> [press Ctrl+D to get back to the command prompt]
 [localhost:~] you% /usr/local/bin/python
 Python 2.3 (#2, Jul 30 2003, 11:45:28)
 [GCC 3.1 20020420 (prerelease)] on darwin
 Type "help", "copyright", "credits", or "license" for more information.
 >>> [press Ctrl+D to get back to the command prompt]
 [localhost:~] you% 





