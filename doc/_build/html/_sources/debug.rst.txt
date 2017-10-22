Outils pour Debug
=================


Debug : Montrer des traces dans une console
-------------------------------------------

Seulement sous Linux

.. code-block:: vbnet

    Sub Debug()
        'Create service
        util = createUnoService("org.universolibre.EasyDev")

        util.debug("Test debug")
    End Sub

.. image:: images/img002.png
    :width: 500px
    :align: center

Sous windows, vous pouvez ouvrir un nouveau document Writer, le sauvegarder
avec comme nom **debug.odt** et montrer des traces de debug dans ce document.

.. image:: images/img003.png
    :width: 500px
    :align: center


Log : Sauvegarder des traces de debug dans un fichier de log
------------------------------------------------------------

.. code-block:: vbnet

    Sub LogFile()

        util = createUnoService("org.universolibre.EasyDev")

        util.log("/home/USER/log.txt", util)

    End Sub

Ajoute automatiquement la date et l'heure dans les traces. ::

    2015-10-28 20:56:35 - EasyDev - <uno_component.EasyDev object at 0x7f96caf34438>
    2015-10-28 20:56:41 - EasyDev - <uno_component.EasyDev object at 0x7f96caf34438>


Msgbox : MessageBox spéciale pour afficher toute sorte de variables
-------------------------------------------------------------------

Afficher tout type de données dans msgbox comme des objets ou des tableaux.

.. code-block:: vbnet

    Sub MessageBox()
        util = createUnoService("org.universolibre.EasyDev")

        'Show info in message box
        util.msgbox("Debug data")

        'Show any data
        data = "This is string"
        util.msgbox(data)

        data = 12345
        util.msgbox(data)

        data = Array("Uno", 2)
        util.msgbox(data)

        util.msgbox(util)
    End Sub


CallMRI : Appeler MRI
---------------------

MRI is the best extension for introspeccion of objects for Apache OpenOffice
and LibreOffice. `Download`_ and install.

Appel à partir d' EasyDev.

.. code-block:: vbnet

    Sub CallMRI()
        util = createUnoService("org.universolibre.EasyDev")

        'MRI is a great extension
        util.mri(util)
    End Sub

.. image:: images/img004.png
    :width: 500px
    :align: center


.. _Download: http://extensions.openoffice.org/en/project/MRI
