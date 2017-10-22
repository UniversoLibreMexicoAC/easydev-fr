Documents
=========

Nouveau document
----------------

Look: `<http://www.openoffice.org/api/docs/common/ref/com/sun/star/frame/XComponentLoader.html>`_

.. code-block:: vbnet

    Sub NewDoc()
        'Create new doc
        util = createUnoService("org.universolibre.EasyDev")

        'Default Calc
        doc = util.newDoc("")

    End Sub

Autres valeurs : swriter, simpress, sdraw, smath

.. code-block:: vbnet

        doc = util.newDoc("sdraw")

Pour un document Base.

.. code-block:: vbnet

    path_db = "/home/USER/dbtest.odb"
    db = util.newDB(path_db)


Obtenir doc
-----------

Courant

.. IMPORTANT::
   Current doc can be IDE

.. code-block:: vbnet

    doc1 = util.getDoc("")
    MsgBox doc1.Title

Obtenir le doc par titre, si pas trouvé, doc est vide

.. code-block:: vbnet

    doc2 = util.getDoc("Name_doc.odt")
    util.msgbox(doc2)


Obtenir le type
---------------

Valeurs retournées : calc, writer, impress, draw, math, base, ide

.. code-block:: vbnet

    doc1 = util.newDoc("sdraw")
    MsgBox util.getTypeDoc(doc1)

    doc2 = util.newDoc("swriter")
    MsgBox util.getTypeDoc(doc2)


Obtenir les documents
---------------------

Obtenir tous les documents ouverts

.. code-block:: vbnet

    docs = util.getDocs()
    MsgBox util.format("{} Open documents", util.len(docs))


Ouvrir
------

Plus d'infos et d'options:

    * `Component Loader <http://api.libreoffice.org/docs/idl/ref/interfacecom_1_1sun_1_1star_1_1frame_1_1XComponentLoader.html>`_
    * `Media Descriptor <http://api.libreoffice.org/docs/idl/ref/servicecom_1_1sun_1_1star_1_1document_1_1MediaDescriptor.html>`_

Ouvrir par le chemin du document

.. code-block:: vbnet

    Dim options1(0) As New com.sun.star.beans.NamedValue
    util = createUnoService("org.universolibre.EasyDev")

    path = "/home/USER/Plantilla.ods"
    options = Array()
    doc = util.openDoc(path, options)

Ouvrir comme modèle

.. code-block:: vbnet

    options1(0).Name = "AsTemplate"
    options1(0).Value = True
    path = "/home/USER/Plantilla.ods"
    doc = util.openDoc(path, options1)

Ouvrir caché

.. code-block:: vbnet

    options1(0).Name = "Hidden"
    options1(0).Value = True
    path = "/home/USER/Plantilla.ods"
    doc = util.openDoc(path, options1)
    MsgBox "Close doc"
    doc.dispose()


Active
------

Donner le focus à un document

.. code-block:: vbnet

    doc1 = util.newDoc("")
    doc2 = util.newDoc("swriter")
    wait(1000)
    util.setFocus(doc1)


Barre de progression
--------------------

Mettre du texte et montrer une barre de progression

.. code-block:: vbnet

    'Get current doc
    doc = util.getDoc("")
    'Get status bar
    sb = util.getStatusBar(doc)

    'Init text and up limit
    sb.start( "Row ", 10 )
    For co1 = 1 To 10
        'Set value
        sb.setValue( co1 )
        Wait 1000
    Next
    'Is import free status bar
    sb.end()


Rendre visible
--------------

Cacher document.

.. code-block:: vbnet

    util = createUnoService("org.universolibre.EasyDev")

    doc = util.newDoc("")

    util.setVisible(doc, False)

    MsgBox "Document is hidden"

    util.setVisible(doc, True)


Exporter PDF
------------

Toutes les options dans `PDF Export <http://wiki.services.openoffice.org/wiki/API/Tutorials/PDF_export>`_ in wiki.

Si l'export est correct, retourne le chemin du PDF sauvegardé..

Exporter le document courant dans le même dossier et le même nom.

.. code-block:: vbnet

    doc = util.getDoc("")
    path = util.exportPDF(doc, "", Array())
    MsgBox util.format("PDF export in: {}", path)

Pour sauvegarder dans un autre dossier et un autre nom.

.. code-block:: vbnet

    path_save = "/home/USER/OTHER_FOLDER"
    path_pdf = util.exportPDF(doc, path_save, Array())


Exporter avec des options

.. code-block:: vbnet

    Dim options(0) As New com.sun.star.beans.NamedValue

    doc = util.getDoc("")
    options(0).Name = "PageRange"
    options(0).Value = "2"
    path = util.exportPDF(doc, "", options)
    MsgBox util.format("PDF export in: {}", path)


Rechercher
----------

.. IMPORTANT::
   Passer un objet correct dans l'argument **Doc**. Voir les exemples.

Rechercher dans Writer

.. code-block:: vbnet

    util = createUnoService("org.universolibre.EasyDev")
    opt = createUnoStruct("org.universolibre.EasyDev.SearchReplace")

    doc = ThisComponent
    opt.Doc = doc
    opt.Search = "test"

    found = util.search(opt)
    util.selectText(doc, found)

Rechercher dans Calc

.. code-block:: vbnet

    util = createUnoService("org.universolibre.EasyDev")
    opt = createUnoStruct("org.universolibre.EasyDev.SearchReplace")

    doc = ThisComponent
    sheet = doc.getCurrentController().getActiveSheet()
    opt.Doc = sheet
    opt.Search = "test"

    found = util.search(opt)
    util.selectRange(doc, found)

Rechercher dans Draw ou Impress

.. code-block:: vbnet

    util = createUnoService("org.universolibre.EasyDev")
    opt = createUnoStruct("org.universolibre.EasyDev.SearchReplace")

    doc = ThisComponent
    page = doc.getDrawPages().getByIndex(0)
    opt.Doc = page
    opt.Search = "test"

    found = util.search(opt)
    util.msgbox(found(0).getString())


