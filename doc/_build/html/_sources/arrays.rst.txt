Tableaux
========

Append : Ajouter un élément
---------------------------

.. code-block:: vbnet

    a = Array("Nikole","Scarlett","Monica","Naomi","Marion")
    a = util.append(a, "Sofia")
    util.msgbox( a )

Delete : Supprimer un élément
-----------------------------

.. code-block:: vbnet

    a = util.delete(a, "Nikole")
    util.msgbox( a )

Extend : Etendre le tableau
---------------------------

.. code-block:: vbnet

    a = Array("Nikole","Scarlett","Monica","Naomi","Marion")
    a2 = Array("Sofia", "Anita")
    a = util.extend(a, a2)
    util.msgbox( a )

Multi : Multiplier
------------------

.. code-block:: vbnet

    a = Array("Nikole","Scarlett","Monica","Naomi","Marion")
    a = util.multi(a, 2)
    util.msgbox( a )

Unique : Valeurs uniques
------------------------

.. code-block:: vbnet

    a = Array(1,2,"Two",3,3,3,4,4,4,4,5,5,5,5,5,"Uno","Uno")
    a = util.unique(a)
    util.msgbox( a )

Reverse : Inverser
------------------

.. code-block:: vbnet

    a = Array("Nikole","Scarlett","Monica","Naomi","Marion")
    a = util.reverse(a)
    util.msgbox( a )

Insert : Insérer un élément à une position
------------------------------------------

.. code-block:: vbnet

    a = Array("Nikole","Scarlett","Monica","Naomi","Marion")
    a = util.insert(a, 2, "Mary")
    util.msgbox( a )

Supprimer un élément à une position
-----------------------------------

.. code-block:: vbnet

    a = Array(1,2,"Two",3,3,3,4,4,4,4,5,5,5,5,5,"Uno","Uno")
    data = util.pop(a, 2)
    util.msgbox( data(0) )  'Tableau sans l'élément supprimé
    util.msgbox( data(1) )  'Elément supprimé

Supprimer le premier élément trouvé

.. code-block:: vbnet

    a = Array(1,2,2,3,3,3,4,4,4,4,5,5,5,5,5,"Uno","Uno")
    util.msgbox( util.remove(a, 5, False) )

Supprimer tous les éléments trouvés

.. code-block:: vbnet

    util.msgbox( util.remove(a, 5, True) )

Len : Taille du tableau
-----------------------

.. code-block:: vbnet

    a = Array(1,2,2,3,3,3,4,4,4,4,5,5,5,5,5,"Uno","Uno")
    util.msgbox( util.len(a) )

Count : Compter un nombre d'éléments du tableau
-----------------------------------------------

.. code-block:: vbnet

    a = Array(1,2,2,3,3,3,4,4,4,4,5,5,5,5,5,"Uno","Uno")
    util.msgbox( util.count(a, 3) )
    util.msgbox( util.count(a, 5) )
    util.msgbox( util.count(a, "Uno") )

Index : Index d'un élément du tableau
-------------------------------------

.. code-block:: vbnet

    a = Array("Nikole","Scarlett","Monica","Naomi","Marion")
    util.msgbox( util.index(a, "Naomi") )
    util.msgbox( util.index(a, "Monica") )

Max, Min and Average : Max, Min et moyenne
------------------------------------------

.. code-block:: vbnet

    a = Array(1,2,3,4,5,6,7,8,9,10)
    util.msgbox( util.max(a) )
    util.msgbox( util.min(a) )
    util.msgbox( util.average(a) )

Sum : Addition
--------------

.. code-block:: vbnet

    a = Array(1,2,3,4,5,6,7,8,9,10)
    util.msgbox( util.sum(a) )

Only sum values, the first element is string

.. code-block:: vbnet

    a = Array("10", 1,2,3,4,5,6,7,8,9,10, "One", "Two")
    util.msgbox( util.sum(a) )

Exists : Test si un élément existe dans le tableau
--------------------------------------------------

.. code-block:: vbnet

    a = Array(1,2,3,4,5,"One","Seven",9,10)
    util.msgbox( util.exists(a, "One") )
    util.msgbox( util.exists(a, "Two") )

Equal : Test d'égalité entre deux tableaux
------------------------------------------

.. code-block:: vbnet

    a1 = Array(1,2,3) : a2 = Array(1,2,3)
    util.msgbox( util.equal(a1, a2) )

    a1 = Array(1,"Dos",3) : a2 = Array(1,2,"Tres")
    util.msgbox( util.equal(a1, a2) )


Slice : Copie
-------------

Recopie d'un tableau dans un autre tableau

.. code-block:: vbnet

    a = Array("Nikole","Scarlett","Monica","Naomi","Marion","Sofia","Anita")
    a2 = util.slice(a, "[:]")
    util.msgbox( a2 )

Les deux premiers éléments

.. code-block:: vbnet

    a2 = util.slice(a, "[:2]")
    util.msgbox( a2 )

Les deux derniers éléments

.. code-block:: vbnet

    a2 = util.slice(a, "[-2:]")
    util.msgbox( a2 )

Copie partielle

.. code-block:: vbnet

    a2 = util.slice(a, "[2:-2]")
    util.msgbox( a2 )

    a2 = util.slice(a, "[::2]")
    util.msgbox( a2 )

    a2 = util.slice(a, "[1::2]")
    util.msgbox( a2 )

Copie inversée

.. code-block:: vbnet

    a2 = util.slice(a, "[::-1]")
    util.msgbox( a2 )


Sorted : Tri de tableau
-----------------------

Tri d'un tableau à une dimension

.. code-block:: vbnet

    a = Array("Nikole","Scarlett","Monica","Naomi","Marion","Sofia","Anita")
    a = util.sorted(a, 0)
    util.msgbox( a )

Tri d'un tableau à plusieurs dimensions

.. code-block:: vbnet

    a = Array( _
        Array(1, 1, 3, "a", 56), _
        Array(1, 2, 3, "z", 43), _
        Array(1, 3, 3, "g", 78), _
        Array(1, 4, 3, "e", 32), _
        Array(1, 5, 3, "M", 89) _
    )
    a = util.sorted(a, 0)
    util.msgbox( a )
    a = util.sorted(a, 1)
    util.msgbox( a )
    a = util.sorted(a, 2)
    util.msgbox( a )
    a = util.sorted(a, 3)
    util.msgbox( a )
    a = util.sorted(a, 4)
    util.msgbox( a )

GetColumn : Obtenir la colonne

.. code-block:: vbnet

    util.msgbox(util.getColumn(a, 1))


Operations
----------

.. code-block:: vbnet

    Sub ArraysOperations()
        util = createUnoService("org.universolibre.EasyDev")

        a1 = Array(1,2,3,4,5) : a2 = Array(3,4,5,6,7,8)
        a = util.union(a1, a2)
        util.msgbox( a )

        a = util.intersection(a1, a2)
        util.msgbox( a )

        a = util.difference(a1, a2)
        util.msgbox( a )

        a = util.symmetricDifference(a1, a2)
        util.msgbox( a )

    End Sub

