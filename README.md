libMysql - a php mysql client library
=====================================

This is a simple php library to make it easy to interface with a Mysql database.

Installation
------------

Place the following two files anywhere from where you can "include" or "require" them:

* class.mysql.php
* config.mysql.php

Now edit config.mysql.php and replace all the configuration values with your database credentials.

Example
-------

Include the library from wherever you placed it:

    require_once(dirname(__FILE__)."/lib/class.mysql.php");

Create a new Mysql instance, and test it:

    $mysql = new Mysql();

    if (!$mysql) {
        die("Cannot initiate Mysql class: ".$mysql->error);
    }

### Select

Retrieve an entire table as an array of objects:

    $rows = $mysql->select('table_name', array('field1_name', 'field2_name', 'field3_name'));

 Retrieve a selection from a table, all the records with field1_name == value1

    $rows = $mysql->select('table_name', array('field1_name', 'field2_name', 'field3_name'),
                                         array('field1_name'=>'value1'));

Multiple WHERE conditions gets AND between them:

    $rows = $mysql->select('table_name', array('field1_name', 'field2_name', 'field3_name'),
                                         array('field1_name'=>'value1', 'field2_name'=>'value2'));

But what if you want to use something other than equality in your conditions?

    $rows = $mysql->select('table_name', array('field1_name', 'field2_name', 'field3_name'),
                                         array('field1_name'=>'value1', 'field2_name'=>'value2'),
                                         array('field1_name'=>'>', 'field2_name'=>'='));

This expands to WHERE `field1_name`>'value1' AND `field2_name`='value2'

### Inserting

    $success = $mysql->insert('table_name', array('field1_name'=>'value1', 'field2_name'=>'value2', 'field3_name'=>'value3'));

    if (!$success) {
        die("Cannot insert new record: ".$mysql->error);
    }

    echo "Amount of rows affected by INSERT: ".$mysql->affected_rows()."\n";
    echo "AUTO_INCREMENT field generated for this INSERT: ".$mysql->inserted_id()."\n";

### Updating

    $success = $mysql->update('table_name', array('field1_name'=>'value1', 'field2_name'=>'value2', 'field3_name'=>'value3'),
                                            array('field1_name'=>'value_old'));

    if (!$success) {
        die("Cannot update records: ".$mysql->error);
    }

    echo "Amount of rows affected by UPDATE: ".$mysql->affected_rows();
