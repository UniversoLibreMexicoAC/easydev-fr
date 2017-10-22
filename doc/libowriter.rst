Writer
======

Paragraphes
----------

Récupérer tous les paragraphes dans un document.

.. code-block:: vbnet

    Sub GetParagraps()
        util = createUnoService("org.universolibre.EasyDev")

        'Get current doc
        doc = util.getDoc("")

        'Get all paragraphs
        paragraphs = util.getParagraphs(doc, True)
        util.msgbox(util.len(paragraphs))

    End Sub

Récupérer les paragraphes avec le texte

.. code-block:: vbnet

    paragraphs = util.getParagraphs(doc, False)
    util.msgbox(util.len(paragraphs))


