Fenêtres de dialogue
====================

Création de fenêtres de dialogue
--------------------------------

Création d'une fenêtre de dialogue à partir d'un fichier.

.. image:: images/img010.png
    :width: 400px
    :align: center

.. code-block:: vbnet

    Sub CreateDialog
        util = createUnoService("org.universolibre.EasyDev")

        path = "/home/USER/dlg_test.xdl"
        dlg = util.createDialog(path)
        dlg.execute()
        dlg.dispose()
    End Sub

Création d'une fenêtre de dialogue à partir d'une bibliothèque; celle par défaut est **Standard**

.. code-block:: vbnet

    macro = createUnoStruct("org.universolibre.EasyDev.Macro")
    macro.Dialog = "Dialog1"

    dlg = util.createDialog(macro)

    'Use other library
    macro.Library = "MyLibrary"
    macro.Dialog = "MyDialog"

    dlg = util.createDialog(macro)

.. NOTE::
    Si la fenêtre de dialogue est dans un document, utiliser la méthode createUnoDialog
    


Label hyperlien
---------------

Evénément souris dessus créé automatiquement

.. image:: images/img011.png
    :width: 350px
    :align: center

.. code-block:: vbnet

    path = "/home/USER/dlg_test.xdl"
    dlg = util.createDialog(path)

    properties = Array( _
        Array("Name", "link_home"), _
        Array("PositionX", 100), _
        Array("PositionY", 10), _
        Array("URL", "http://universolibre.org"), _
        Array("Label", "http://universolibre.org"), _
    )
    util.createControl(dlg, "FixedHyperlink", properties)
    dlg.execute()
    dlg.dispose()


Roadmap
-------

Ajouter des options de menus

.. image:: images/img012.png
    :width: 200px
    :align: center

.. code-block:: vbnet

    path = "/home/USER/dlg_test.xdl"
    dlg = util.createDialog(path)

    options = Array("Init", "Values", "Config", "Other")
    properties = Array( _
        Array("Name", "roadmap"), _
        Array("Width", 50), _
        Array("Height", 150), _
        Array("Options", options), _
    )
    util.createControl(dlg, "Roadmap", properties)
    dlg.execute()
    dlg.dispose()

.. _grid:

Grille
------

Créer une grille et mettre des données d'un tableau. Détecter les valeurs de colonnes et le format.

.. image:: images/img013.png
    :width: 300px
    :align: center

.. code-block:: vbnet

    c1 = Array( _
        Array("Title", "State"), _
        Array("HorizontalAlign", 0), _
    )
    c2 = Array( _
        Array("Title", "People"), _
        Array("HorizontalAlign", 2), _
        Array("Identifier", True), _
    )
    columns = Array(c1, c2)
    properties = Array( _
        Array("Name", "grid"), _
        Array("PositionX", 100), _
        Array("PositionY", 50), _
        Array("Step", 4), _
        Array("Columns", columns), _
    )
    grid = util.createControl(dlg, "Grid", properties)

    data = Array( _
        Array("Uno", 2222), _
        Array("Tres", 44444), _
        Array("Cinco", 666666), _
        Array("Siete", 666666), _
    )
    col_format = Array()
    util.setGridData(grid, data, col_format)

    dlg.execute()
    dlg.dispose()

Ajouter des données à une plage de cellules.

.. code-block:: vbnet

    data = ThisComponent.getCurrentSelection().getDataarray()
    col_format = Array()
    util.setGridData(grid, data, col_format)

Définir des données à partir d'une requête, voir :ref:`base-query`.

.. code-block:: vbnet

    odbc = "TESTODBCSQLITE"
    user = ""
    passw = ""

    con = util.conODBC(odbc, user, passw)

    sql = "SELECT id, name FROM contactos"
    data = util.query(con, sql, False)
    properties = Array( _
        Array("Name", "grid"), _
        Array("PositionX", 10), _
        Array("PositionY", 10), _
        Array("Columns", Array()) _
    )
    grid = util.createControl(dlg, "Grid", properties)
    util.setQuery(grid, data, True)

Changer le format par défaut pour les colonnes avec valeurs.

.. code-block:: vbnet

    data = ThisComponent.getCurrentSelection().getDataarray()

    'Default format
    util.numfmt = "$ {0:,.2f}"

    col_format = Array()
    util.setGridData(grid, data, col_format)

Ou changer le format pour chaque colonne.

.. code-block:: vbnet

    data = ThisComponent.getCurrentSelection().getDataarray()
    col_format = Array("{}", "$ {0:,.2f}")
    util.setGridData(grid, data, col_format)

et obtenir la grille de données en tableau.

.. code-block:: vbnet

    data = util.getGridData(grid, Array())
    util.msgbox(data)






TextBox
-------

Créer une text box, automatic changer couleur de fond sur focus.

.. image:: images/img014.png
    :width: 300px
    :align: center

.. code-block:: vbnet

    properties = Array( _
        Array("Name", "txt_name"), _
        Array("PositionX", 10), _
        Array("PositionY", 10), _
    )
    util.createControl(dlg, "Edit", properties)
    dlg.execute()
    dlg.dispose()

Vous pouvez changer la couleur de fond par défaut. Changer la couleur avant la création du contrôle.

.. image:: images/img015.png
    :width: 300px
    :align: center

.. code-block:: vbnet

    util.colorOnFocus = RGB(229, 255, 204)


CommandButton
-------------

Créer un bouton de commande et lui assigner une macro à exécuter. La bibliothèque par défaut est **Standard**.
Par défaut, le nom de la macro : **CONTROL_NAME + _action**, dans cet exemple:

.. code-block:: vbnet

    Sub cmd_test_action(event):
        MsgBox event.Source.Model.Name
    End Sub

Argument **event** is important.

.. code-block:: vbnet

    macro.Language = "Basic"
    macro.Module = "LODialog"
    properties = Array( _
        Array("Name", "cmd_test"), _
        Array("PositionX", 10), _
        Array("PositionY", 60), _
        Array("Macro", macro), _
    )
    util.createControl(dlg, "Button", properties)
