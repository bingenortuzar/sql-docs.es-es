---
title: Execute, Requery y Clear métodos ejemplo (JScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- Requery method [ADO], JScript example
- Clear method [ADO], JScript example
- Execute method [ADO], JScript example
ms.assetid: 51a87e91-c9d9-4e49-af47-79cce2c4cfe0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4ceafffc9d6b87428ae3da58a2f824bb7ed3c34
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918818"
---
# <a name="execute-requery-and-clear-methods-example-jscript"></a>Execute, Requery y Clear métodos ejemplo (JScript)
Este ejemplo se muestra el **Execute** método cuando se ejecuta desde ambos un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto y un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto. También usa el [Requery](../../../ado/reference/ado-api/requery-method.md) método para recuperar los datos actuales en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)y el [borrar](../../../ado/reference/ado-api/clear-method-ado.md) método para borrar el contenido de la [errores](../../../ado/reference/ado-api/errors-collection-ado.md)colección. (El **errores** accedan a la colección a través de la **conexión** objeto de la [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).) Nombre del archivo **ExecuteJS.asp al**.  
  
```  
<!-- BeginExecuteJS -->  
<%@LANGUAGE="JScript"%>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<%  
    strLastName = new String(Request.Form("AuthorLName"));  
  
    if (strLastName.indexOf("undefined") > -1)  
        strLastName = "";  
%>  
  
<html>  
  
<head>  
<title>Execute, Requery and Clear Methods Example (JScript)</title>  
<style>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
-->  
</style>  
</head>  
  
<body bgcolor="White">  
<h1>Execute, Requery and Clear Methods Example (JScript)</h1>  
<%  
    if (strLastName.length > 0)  
    {  
        // command and recordset variables  
        var Connect = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='pubs';Integrated Security='SSPI';";  
        var Cnxn = Server.CreateObject("ADODB.Connection");  
        var cmdAuthor = Server.CreateObject("ADODB.Command");  
        var rsAuthor = Server.CreateObject("ADODB.Recordset");  
        var rsAuthor2 = Server.CreateObject("ADODB.Recordset");  
        var SQLAuthor2, strMessage, strMessage2;  
        var Err, ErrCount;  
  
        try  
        {  
            // open connection  
            Cnxn.Open(Connect);  
  
            // command object parameters  
            cmdAuthor.CommandText = "SELECT * FROM Authors WHERE au_lname = ?";  
            cmdAuthor.Parameters.Append(cmdAuthor.CreateParameter("Last Name", adChar, adParamInput, 20, strLastName));  
            cmdAuthor.ActiveConnection = Cnxn;  
  
            // recordset from command.execute  
            rsAuthor = cmdAuthor.Execute();  
  
            // recordset from connection.execute  
            SQLAuthor2 = "SELECT * FROM Authors";  
            rsAuthor2 = Cnxn.Execute(SQLAuthor2);  
  
                // check for errors  
                ErrCount = Cnxn.errors.count;  
                if(ErrCount !== 0) //write the errors  
                {  
                    for(Err = 0; Err = ErrCount; Err++){  
                        Err = Cnxn.errors.item;  
                        Response.Write(Err);  
                    }  
                    // clean out any existing errors  
                    Cnxn.Errors.Clear;  
                }  
  
                // show the data      
            Response.Write("<HR><HR>");  
  
                // first recordset  
            Response.Write("<b>Command.Execute results</b>")  
            while (!rsAuthor.EOF)  
            {  
                // build output string by starting a new line  
                strMessage = "<P>";  
                strMessage += "<br>";  
  
                // recordset data   
                strMessage += rsAuthor("au_fname") + " ";   
                strMessage += rsAuthor("au_lname") + " ";  
  
                // end the line  
                strMessage += "</P>";  
  
                // show the results  
                Response.Write(strMessage);  
  
                // get next record  
                rsAuthor.MoveNext;  
            }  
  
            Response.Write("<HR><HR>");  
  
            // second recordset  
            Response.Write("<b>Connection.Execute results</b>")  
            while (!rsAuthor2.EOF)  
            {  
                // start a new line  
                strMessage2 = "<P>";  
  
                // first and last name are in first column  
                strMessage2 += rsAuthor2("au_fname") + " "   
                strMessage2 += rsAuthor2("au_lname") + " ";  
  
                // end the line  
                strMessage2 += "</P>";  
  
                // show results  
                Response.Write(strMessage2);  
  
                // get next record  
                rsAuthor2.MoveNext;  
            }  
        }  
        catch (e)  
        {  
            Response.Write(e.message);  
        }  
        finally  
        {  
            // clean up  
            if (rsAuthor.State == adStateOpen)  
                rsAuthor.Close;  
            if (rsAuthor2.State == adStateOpen)  
                rsAuthor2.Close;  
            if (Cnxn.State == adStateOpen)  
                Cnxn.Close;  
            rsAuthor1 = null;  
            rsAuthor2 = null;  
            Cnxn = null;  
        }  
    }  
%>  
  
<hr>  
  
<form method="POST" action="ExecuteJS.asp" id=form1 name=form1>  
  <p align="left">Enter last name of author to find (e.g., Ringer): <input type="text" name="AuthorLName" size="40"></p>  
  <p align="left"><input type="submit" value="Submit" name="B1"><input type="reset" value="Reset" name="B2"></p>  
</form>  
</body>  
  
</html>  
<!-- EndExecuteJS -->  
```  
  
## <a name="see-also"></a>Vea también  
 [Clear (método) (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Objeto de error](../../../ado/reference/ado-api/error-object.md)   
 [Método Execute (Command ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Ejecutar el método (conexión de ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Requery (método)](../../../ado/reference/ado-api/requery-method.md)
