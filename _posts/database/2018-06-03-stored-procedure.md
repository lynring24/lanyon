---
layout: post
title: stored procedure
categories: database
---

{% highlight jsp %}

CREATE OR REPLACE PROCEDURE pName (
  inputName IN dataType,
  outputName OUT dataType,
  inOutPutName INOUT datatype
  )
IS
  declareVariable Type%ROWTYPE;
BEGIN
  // PL/SQL BLOCK
  SELECT *
  INTO declareVariable
  FROM tableName;
END;
/

CREATE OR REPLACE FUNCTION fName (
  inputName IN dataType,
  inputName IN dataType
  )
RETURN returnDataType  
IS
    declareVariable Type%ROWTYPE;
BEGIN
  // PL/SQL BLOCK
  SELECT *
  INTO declareVariable
  FROM tableName;

    RETURN declareVariable;
END;
/

CREATE OR REPLACE TRIGGER tName
BEFORE|AFTER
[UPDATE OR DELETE OR INSERT] ON tableName
[FOR EACH ROW] -- if row operation
DECLARE
   declareVariable TYPE;
BEGIN
[WHEN CONDITION]
  DBMS_OUTPUT.PUT_LINE(:old.column);
  DBMS_OUTPUT.PUT_LINE(:new.column);  
END;
/

























{% endhighlight jSP %}
