
.. raw:: html

   <h1 align="center">

Lab: Connect to Db2 database on Cloud using Python

.. raw:: html

   </h1>

Introduction
============

This notebook illustrates how to access DB2 Warehouse on Cloud using
Python by following the steps below: 1. Import the ``ibm_db`` Python
library 1. Enter the database connection credentials 1. Create the
database connection 1. Close the database connection

**Notice:** Please follow the instructions given in the first Lab of
this course to Create a database service instance of Db2 on Cloud and
retrieve your database credentials.

Import the ``ibm_db`` Python library
------------------------------------

The ``ibm_db`` `API <https://pypi.python.org/pypi/ibm_db/>`__ provides a
variety of useful Python functions for accessing and manipulating data
in an IBM® data server database, including functions for connecting to a
database, preparing and issuing SQL statements, fetching rows from
result sets, calling stored procedures, committing and rolling back
transactions, handling errors, and retrieving metadata.

We first import the ibm\_db library into our Python Application

Execute the following cell by clicking within it and then press shift
and enter keys simultaneously

.. code:: ipython3

    import ibm_db

When the command above completes, the ``ibm_db`` library is loaded in
your notebook.

Identify the database connection credentials
--------------------------------------------

Connecting to dashDB or DB2 database requires the following information:
\* Driver Name \* Database name \* Host DNS name or IP address \* Host
port \* Connection protocol \* User ID (or username) \* User Password

**Notice:** To obtain credentials please refer to the instructions given
in the first Lab of this course

Now enter your database credentials below

Replace the placeholder values in angular brackets <> below with your
actual database credentials

e.g. replace "< database >" with "BLUDB"

.. code:: ipython3

    dsn_driver = "{IBM DB2 ODBC DRIVER}"
    dsn_database = "<database>"            # e.g. "BLUDB"
    dsn_hostname = "<hostname>" # e.g.: "awh-yp-small03.services.dal.bluemix.net"
    dsn_port = "<port>"                # e.g. "50000" 
    dsn_protocol = "<protocol>"            # i.e. "TCPIP"
    dsn_uid = "<username>"        # e.g. "dash104434"
    dsn_pwd = "<password>"       # e.g. "7dBZ3wWt9XN6$o0JiX!m"

Create the DB2 database connection
----------------------------------

Ibm\_db API uses the IBM Data Server Driver for ODBC and CLI APIs to
connect to IBM DB2 and Informix.

Lets build the dsn connection string using the credentials you entered
above

.. code:: ipython3

    #Create the dsn connection string
    dsn = (
        "DRIVER={0};"
        "DATABASE={1};"
        "HOSTNAME={2};"
        "PORT={3};"
        "PROTOCOL={4};"
        "UID={5};"
        "PWD={6};").format(dsn_driver, dsn_database, dsn_hostname, dsn_port, dsn_protocol, dsn_uid, dsn_pwd)
    
    #print the connection string to check correct values are specified
    print(dsn)

Now establish the connection to the database

.. code:: ipython3

    #Create database connection
    
    try:
        conn = ibm_db.connect(dsn, "", "")
        print ("Connected!")
    
    except:
        print ("Unable to connect to database")
    


Close the Connection
--------------------

We free all resources by closing the connection. Remember that it is
always important to close connections so that we can avoid unused
connections taking up resources.

.. code:: ipython3

    ibm_db.close(conn)

Summary
-------

In this tutorial you established a connection to a DB2 Warehouse on
Cloud database from a Python notebook using ibm\_db API.

Copyright © 2017
`cognitiveclass.ai <cognitiveclass.ai?utm_source=bducopyrightlink&utm_medium=dswb&utm_campaign=bdu>`__.
This notebook and its source code are released under the terms of the
`MIT License <https://bigdatauniversity.com/mit-license/>`__.
