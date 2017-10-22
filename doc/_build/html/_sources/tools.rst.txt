Outils
======


Récupérer infos PC
------------------

.. code-block:: vbnet

    Sub ShowInfoPC()
        util = createUnoService("org.universolibre.EasyDev")

        'Système d'exploitation
        util.msgbox(util.OS)

        'Nom de l''aplication
        util.msgbox(util.APP_NAME)

        'Version de l'application
        util.msgbox(util.APP_VERSION)

        'Langage de l''application
        util.msgbox(util.LANGUAGE)

        'Taille Ecran
        util.msgbox(util.getSizeScreen())

        ' https://docs.python.org/3.3/library/platform.html
        ' Get info PC:
        ' name user,
        ' name pc
        ' system/OS name,
        ' machine type,
        ' Returns the (real) processor name
        ' string identifying platform with as much useful information as possible,
        util.msgbox(util.getInfoPC())
    End Sub


Poser une question
------------------

.. code-block:: vbnet

    Sub Question()
        util = createUnoService("org.universolibre.EasyDev")

        title = "My App"
        message = "Is easy Python?"
        res = util.question(title, message)

        'If Yes return True, else return False
        util.msgbox(res)

    End Sub


Rendu de chaîne
---------------

Rendu de texte avec remplacement d'arguments.

.. code-block:: vbnet

    Sub RenderString()
        util = createUnoService("org.universolibre.EasyDev")

        'Used NamedValue
        message = "Hello $data with $language, from Basic 1!!"
        Dim data1(1) As New com.sun.star.beans.NamedValue

        data1(0).Name = "data"
        data1(0).Value = "World"
        data1(1).Name = "language"
        data1(1).Value = "Python"
        message = util.render(message, data1)
        util.msgbox(message)

        'Used PropertyValue
        message = "Hello $data with $language, from Basic 2!!"
        Dim data2(1) As New com.sun.star.beans.PropertyValue

        data2(0).Name = "data"
        data2(0).Value = "World"
        data2(1).Name = "language"
        data2(1).Value = "Python"
        message = util.render(message, data2)
        util.msgbox(message)

        'Used Arrays
        message = "Hello $data with $language, from Basic 3!!"
        data = Array( _
            Array("data", "World"), _
            Array("language", "Python") _
        )
        message = util.render(message, data2)
        util.msgbox(message)

    End Sub


Format
------

Voir plus d'info et d'exemples  `here`_.

.. code-block:: vbnet

    Sub FormatData()
        util = createUnoService("org.universolibre.EasyDev")

        MsgBox util.format("Hello {}", "World")

        MsgBox util.format("Hello {} from {}", Array("World", "PyUNO"))

        MsgBox util.format("Hello {1} from {0}", Array("World", "PyUNO"))

        MsgBox util.format("{:<20}|{:^20}|{:>20}", Array("Left", "Center", "Rigth"))

        MsgBox util.format("{:_<20}|{:-^20}|{:_>20}", Array("Left", "Center", "Rigth"))

        MsgBox util.format("{:d} {:f}", Array(100, 3.1416))

        MsgBox util.format("{0:,.2f}", 123456789.2468)

        MsgBox util.format("Number {n1} y {n2}", Array(Array("n1", "one"), Array("n2", "two")))

        MsgBox util.format("Number {n2} y {n1}", Array(Array("n1", "one"), Array("n2", "two")))

        my_date = createUnoStruct("com.sun.star.util.Date")
        my_date.Day = 15
        my_date.Month = 1
        my_date.Year = 1974
        MsgBox util.format("{:%d-%B-%Y}", my_date)

        my_date = createUnoStruct("com.sun.star.util.DateTime")
        my_date.Day = 15
        my_date.Month = 1
        my_date.Year = 1974
        my_date.Hours = 13
        my_date.Minutes = 30

        MsgBox util.format("{:%Y-%b-%d %H:%M}", my_date)

    End Sub


Fichiers et répertoires
-----------------------

Retourner le nom du chemin dans la config. Voir `XPathSettings`_.

.. code-block:: vbnet

    path = util.getPath("Temp")
    util.msgbox(path)
    path = util.getPath("Work")
    util.msgbox(path)

Obtenir des infos du chemin: base, nom, nom sans extension, extension

.. code-block:: vbnet

    data = util.getPathInfo("/home/USER/log.txt")
    util.msgbox(data)


Joindre des chemins

.. code-block:: vbnet

    path = util.pathJoin(Array("/home", "USER", "Documents"))
    util.msgbox(path)
    path = util.pathJoin(Array("/home/USER/Documents", "..", "Picture"))
    util.msgbox(path)

Sélectionner un répertoire, répertoire par défaut des documents user

.. code-block:: vbnet

    folder = util.getFolder("")
    util.msgbox(folder)

    'With other init folder
    folder = util.getFolder("/home/USER")
    util.msgbox(folder)

Sélectionner un fichier sans filtre

.. code-block:: vbnet

    file = util.getSelectedFiles("", False, Array())
    util.msgbox(file)

Selectionner plusieurs fichiers

.. code-block:: vbnet

    files = util.getSelectedFiles("", True, Array())
    util.msgbox(files)

Sélectionner plusieurs fichiers avec filtre

.. code-block:: vbnet

    filters = Array( _
        Array("TXT", "*.txt"), _
        Array("LOG", "*.log"), _
        Array("CER | KEY", "*.cer;*.key") _
    )
    files = util.getSelectedFiles("", True, filters)
    util.msgbox(files)

Obtenir tous les fichiers récursivement

.. code-block:: vbnet

    files = util.getFiles("/home/USER/Pictures", "")
    util.msgbox(files)

Obtenir tous les fichiers avec une extension

.. code-block:: vbnet

    files = util.getFiles("/home/USER/Pictures", "jpg")
    util.msgbox(files)
    files = util.getFiles("/home/USER/Pictures", "png")
    util.msgbox(files)

Ouvrir un fichier et lire tout son contenu

.. code-block:: vbnet

    data = util.fileOpen("/home/USER/log.txt", "r", False)
    util.msgbox(data)

Ouvrir un fichier, lire les lignes dans un tableau

.. code-block:: vbnet

    data = util.fileOpen("/home/USER/log.txt", "r", True)
    util.msgbox(data)

Sauvegarder les données dans un nouveau fichier
.. code-block:: vbnet

    data = "Hello World Python"
    util.fileSave("/home/USER/test.txt", "w", data)
    'Verify
    data = util.fileOpen("/home/mau/test.txt", "r")
    util.msgbox(data)

Sauvegarder les données en les ajoutant à un fichier

.. code-block:: vbnet

    data = "Hello World Python" & CHR(10)
    util.fileSave("/home/USER/test2.txt", "a", data)
    'Verify
    data = util.fileOpen("/home/USER/test2.txt", "r")
    util.msgbox(data)


Exécuter
--------

Exécuter une commande et attendre la réponse

.. code-block:: vbnet

    res = util.execute(Array("ls","-la"), True)
    util.msgbox(res)

Exécuter une commande sans attendre

.. code-block:: vbnet

    util.execute(Array("gnome-calculator"), False)


Config
------

Sauvegarder une valeur dans la config en permanence

.. code-block:: vbnet

    util.setConfig("DefaultMail", "test@correolibre.net")
    'Get value from config
    value = util.getConfig("DefaultMail")
    util.msgbox(value)

Il est possible de sauvegarder des tableaux

.. code-block:: vbnet

    util.setConfig("Matriz", Array(1,2,3))
    value = util.getConfig("Matriz")
    util.msgbox(value)


Clipboard
---------

Récupérer du texte du presse-papier

.. code-block:: vbnet

    value = util.getClipboard()
    util.msgbox(value)

Envoyer du texte au presse-papier

.. code-block:: vbnet

    util.setClipboard("Hello World PyUNO!!")
    'Verify
    value = util.getClipboard()
    util.msgbox(value)

Copier, coller. Actuellement seulement avec Calc. Copie la sélection courante.

.. code-block:: vbnet

    util = createUnoService("org.universolibre.EasyDev")

    doc = ThisComponent
    util.copy(doc)
    util.paste(doc)

.. image:: images/img021.png
    :width: 300px
    :align: center

Copier et coller des plages de cellules. C'est très important, selectionner les plages correctement. Voir :ref:`getranges`.

.. code-block:: vbnet

    util = createUnoService("org.universolibre.EasyDev")
    source = createUnoStruct("org.universolibre.EasyDev.CellRangeAddress")
    target = createUnoStruct("org.universolibre.EasyDev.CellRangeAddress")

    doc = ThisComponent
    source.Doc = doc
    source.Sheet = "Sheet1"
    source.Name = "A1:B2"
    range = util.getRange(source)
    util.selectRange(doc, range)
    util.copy(doc)

    target.Doc = doc
    target.Sheet = "Sheet1"
    target.Name = "A8"
    range = util.getRange(target)
    util.selectRange(doc, range)
    util.paste(doc)

.. image:: images/img022.png
    :width: 200px
    :align: center


Unix time
---------

Look `<https://en.wikipedia.org/wiki/Unix_time>`_

.. code-block:: vbnet

    epoch = util.getEpoch()
    util.msgbox(epoch)


Call macros
-----------

Look: `Scripting Framework <https://wiki.openoffice.org/wiki/Documentation/DevGuide/Scripting/Scripting_Framework_URI_Specification>`_

Pour le test sauvegarder la macro suivante dans:

``/home/USER/.config/libreoffice/4/user/Scripts/python/mymacros.py``
::

    import uno
    import time

    def show_time(cell):
        cell.setString(time.strftime('%c'))
        time.sleep(3)
        return

Appeler une macro en Python (c'est le défaut), attendre la fin.

.. code-block:: vbnet

    macro = createUnoStruct("org.universolibre.EasyDev.Macro")
    macro.Library = "mymacros"
    macro.Name = "show_time"
    cell = ThisComponent.CurrentSelection
    util.callMacro(macro, Array(cell))

.. image:: images/img005.png
    :width: 400px
    :align: center

Appeler une macro en Python, sans attendre la fin

.. code-block:: vbnet

    macro = createUnoStruct("org.universolibre.EasyDev.Macro")
    macro.Library = "mymacros"
    macro.Name = "show_time"
    macro.Thread = True
    cell = ThisComponent.CurrentSelection
    util.callMacro(macro, Array(cell))

Appeler une macro en Basic

.. code-block:: vbnet

    macro = createUnoStruct("org.universolibre.EasyDev.Macro")
    macro.Library = "EasyDevLib"
    macro.Module = "Examples"
    macro.Name = "HelloWorld"
    macro.Language = "Basic"
    macro.Thread = False
    util.callMacro(macro, Array())

.. image:: images/img006.png
    :width: 150px
    :align: center


Timer
-----

Sauvegarder la macro suivante dans : 

``/home/USER/.config/libreoffice/4/user/Scripts/python/mymacros.py``
::

    import uno
    import time

    def show_time(cell):
        cell.setString(time.strftime('%c'))
        return

timer(NAME_TIMER, SECONDS_WAIT, MACRO, ARGUMENTS)

NAME_TIMER est important pour arrêter le timer. Timer s'exécute toujours dans un autre thread.

.. code-block:: vbnet

    util = createUnoService("org.universolibre.EasyDev")

    'Make data macro
    macro = createUnoStruct("org.universolibre.EasyDev.Macro")
    macro.Library = "mymacros"
    macro.Name = "show_time"
    'Arguments
    cell = ThisComponent.CurrentSelection
    'Timer name "time" and wait one second
    util.timer("time", 1, macro, Array(cell))

Arrêter le timer par le nom

.. code-block:: vbnet

    Sub StopTimer()
        util = createUnoService("org.universolibre.EasyDev")
        util.stopTimer("time")
    End Sub


Export CSV
----------

Definir la plage avec données et sélection.

.. image:: images/img007.png
    :width: 400px
    :align: center

et exporter

.. code-block:: vbnet

    util = createUnoService("org.universolibre.EasyDev")

    range = ThisComponent.CurrentSelection

    path = "/home/USER/test.csv"
    data = range.getDataArray()
    options = Array()

    util.exportCSV(path, data, options)

Changer les options pour l'export, look: `<https://docs.python.org/3.3/library/csv.html#csv.writer>`_

.. code-block:: vbnet

    Dim options(0) As New com.sun.star.beans.NamedValue

    util = createUnoService("org.universolibre.EasyDev")

    range = ThisComponent.CurrentSelection

    path = "/home/USER/test.csv"
    data = range.getDataArray()
    options(0).Name = "delimiter"
    options(0).Value = "|"
    util.exportCSV(path, data, options)


Import CSV
----------

La plage sélectionnée doit être le nombre exact de colonnes et de lignes à 
importer, seulement pour cet exemple.


More options see: `<https://docs.python.org/3.3/library/csv.html#csv.reader>`_

.. image:: images/img016.png
    :width: 400px
    :align: center

et importer

.. code-block:: vbnet

    util = createUnoService("org.universolibre.EasyDev")

    range = ThisComponent.CurrentSelection
    path = "/home/USER/test.csv"
    options = Array()
    data = util.importCSV(path, options)
    range.setDataArray(data)

.. image:: images/img017.png
    :width: 400px
    :align: center

Il est possible de calculer automatiquement la taille de la plage de
données, voir :ref:`setdata` .



Compresser fichiers et dossiers
-------------------------------

Compresser fichier , écrire dans le même répertoire avec le même nom.

.. code-block:: vbnet

    util = createUnoService("org.universolibre.EasyDev")

    source = "/home/mau/Documents/debug.log"
    'Target = "/home/mau/Documents/debug.zip"
    target = ""
    util.zip(source, target)

Compresser fichier dans un autre répertoire, même nom.

.. code-block:: vbnet

    source = "/home/mau/Documents/debug.log"
    'Target = "/home/mau/debug.zip"
    target = "/home/mau"
    util.zip(source, target)

Compresser fichier dans un autre répertoire avec un autre nom.

.. code-block:: vbnet

    source = "/home/mau/Documents/debug.log"
    target = "/home/mau/test.zip"
    util.zip(source, target)

Compresser dossier

.. code-block:: vbnet

    source = "/home/mau/Pictures"
    'Target = "/home/mau/Pictures.zip"
    target = ""
    util.zip(source, target)

    'Target = "/home/mau/Documents/Pictures.zip"
    target = "/home/mau/Documents"
    util.zip(source, target)

    target = "/home/mau/Documents/pic.zip"
    util.zip(source, target)

Unzip
-----

Décompresser fichier, extraire tout le contenu.

.. code-block:: vbnet

    source = "/home/mau/Documents/Pictures.zip"
    target = ""
    file_name = ""
    util.unzip(source, target, file_name)

Extraire dans un autre dossier.

.. code-block:: vbnet

    target = "/home/mau"
    file_name = ""
    util.unzip(source, target, file_name)

Extraire seulement un fichier.

.. code-block:: vbnet

    target = "/home/mau"
    file_name = "mylove.png"
    util.unzip(source, target, file_name)


.. _XPathSettings: http://api.libreoffice.org/docs/idl/ref/interfacecom_1_1sun_1_1star_1_1util_1_1XPathSettings.html
.. _here: https://pyformat.info/
.. _Download: http://extensions.openoffice.org/en/project/MRI
.. _Set data:
