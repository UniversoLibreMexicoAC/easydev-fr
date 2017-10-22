Base de données
===============

Connexion BD
-------------

Connexion à une base de données enregistrée dans Base.

.. code-block:: vbnet

    Sub ConnectDB()
        db_name = "test"
        user = ""
        pass = ""
        con = util.conDB(db_name, user, pass)

        util.msgbox(con.isClosed())
    End Sub

Verifier si la base existe.

.. code-block:: vbnet

    db_name = "test"
    MsgBox util.existsDB(db_name)

Si elle existe, récupérer son chemin.

.. code-block:: vbnet

    db_name = "test"
    If util.existsDB(db_name) Then
        MsgBox util.getPathDB(db_name)
    End If

Créer une B.D et l'enregistrer dans Base.

.. code-block:: vbnet

    path_db = "/home/USER/dbtest.odb"
    db_name = "TestOne"
    util.newDB(path_db)
    util.registerDB(db_name, path_db)

Révoquer une B.D dans Base.

.. code-block:: vbnet

    db_name = "test"
    util.revokeDB(db_name)


ODBC
----

Test connexion avec : MySQL, PostgreSQL, SQLite and MSSQL.

.. code-block:: vbnet

    Sub ConexionODBC()

        util = createUnoService("org.universolibre.EasyDev")

        odbc = "ConSQL"
        user = "sa"
        passw = "letmein"

        con = util.conODBC(odbc, user, passw)

        util.msgbox(con)

    End Sub

.. _base-query:

Requête
-------

Faire une requête, Obtenir des données comme tableaux

.. code-block:: vbnet

    odbc = "ODBCSQLITE"
    user = ""
    passw = ""
    con = util.conODBC(odbc, user, passw)

    sql = "SELECT * FROM contactos"
    data = util.query(con, sql, True)
    util.msgbox(data)

Faire une requête, Obtenir des données comme resulset

.. code-block:: vbnet

    sql = "SELECT * FROM contactos"
    data = util.query(con, sql, False)
    util.msgbox(data)

Vous pouvez définir resulset vers grille, see :ref:`grid`.

Mise à jour
-----------

Insertion de données.

.. code-block:: vbnet

    sql = "INSERT INTO ""directory"" VALUES (6, 'Nikole Kidman', '1970-01-15', 'nikole@correo.com')"
    row = util.update(con, sql)
    util.msgbox(row)

Mise à jour de données.

.. code-block:: vbnet

    sql = "UPDATE ""directory"" SET ""email""='nk@coreo.com' WHERE ""id""=6"
    row = util.update(con, sql)
    util.msgbox(row)

Suppression de données.

.. code-block:: vbnet

    sql = "DELETE FROM ""directory"" WHERE ""id""=5"
    row = util.update(con, sql)
    util.msgbox(row)
