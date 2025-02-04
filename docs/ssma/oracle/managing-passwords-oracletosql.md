---
title: Administración de contraseñas (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Managing Passwords in Oracle, Exporting or Importing Encrypted Password
- Managing passwords in Oracle, Securing Password
ms.assetid: 8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: d8520224662c02d1ffbe9fd2fd6ef76f8b1e698a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262921"
---
# <a name="managing-passwords-oracletosql"></a>Administración de contraseñas (OracleToSQL)
En esta sección es acerca de cómo proteger las contraseñas de la base de datos y el procedimiento para importar o exportar a ellos a través de servidores:  
  
1.  Protección de contraseña  
  
2.  Exportar o importar la contraseña cifrada  
  
## <a name="securing-password"></a>Protección de contraseña  
SSMA permite proteger la contraseña de una base de datos.  
  
Use el procedimiento siguiente para implementar una conexión segura:  
  
Especifique una contraseña válida con uno de los tres métodos siguientes:  
  
1.  **Texto no cifrado:** Escriba la contraseña de la base de datos en el atributo de valor del nodo 'contraseña'. Se encuentra bajo el nodo de definición de servidor en la sección de servidor del archivo de script o archivo de conexión de servidor.  
  
    Las contraseñas en texto no cifrado no son seguras. Por lo tanto, se producirá el siguiente mensaje de advertencia en la salida de consola: *"Servidor &lt;id de servidor&gt; sea la contraseña proporcionada en forma de texto no cifrado no seguras, aplicación de consola de SSMA proporciona una opción para proteger la contraseña a través de cifrado, vea la opción - securepassword en el archivo de ayuda SSMA para obtener más información información".*  
  
    **Contraseñas cifradas:** En este caso, la contraseña especificada, se almacena en un formato cifrado en el equipo local en ProtectedStorage.ssma.  
  
    -   **Protección de contraseñas**  
  
        -   Ejecute el `SSMAforOracleConsole.exe` con el `-securepassword` y agregue el modificador de la línea de comandos pasando el servidor de archivos de conexión o un script que contiene el nodo de contraseña en la sección de definición de servidor.  
  
        -   En el símbolo del sistema, el usuario se le pide que escriba la contraseña de la base de datos y confírmela.  
  
            Los identificadores de definición de servidor y sus correspondientes contraseñas cifradas se almacenan en un archivo en el equipo local  
            
            Ejemplo 1:  
            
                Specify password
                
                C:\SSMA\SSMAforOracleConsole.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx
            
            Ejemplo 2:
            
                C:\SSMA\SSMAforOracleConsole.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
    
    -   **Quitar contraseñas cifradas**  
  
        Ejecute el `SSMAforOracleConsole.exe` con el`-securepassword` y `-remove` cambiar en la línea de comandos pasar los identificadores de servidor, para quitar las contraseñas cifradas desde el archivo de almacenamiento protegido presente en el equipo local.  
        
        Ejemplo:  
        
            C:\SSMA\SSMAforOracleConsole.EXE -securepassword -remove all
            C:\SSMA\SSMAforOracleConsole.EXE -securepassword -remove "source_1,target_1"  
  
    -   **Enumerar los Id. de servidor cuyas contraseñas están cifradas**  
  
        Ejecute el `SSMAforOracleConsole.exe` con el `-securepassword` y `-list` cambiar en la línea de comandos para enumerar todos los identificadores de servidor cuyas contraseñas se han cifrado.  
  
        Ejemplo:  
        
            C:\SSMA\SSMAforOracleConsole.EXE -securepassword -list  
  
    > [!NOTE]  
    > 1.  La contraseña en texto no cifrado que se mencionan en el archivo de conexión de script o un servidor tiene prioridad sobre la contraseña cifrada en el archivo protegido.  
    > 2.  Cuando no existe ninguna contraseña en la sección de servidor del archivo de conexión de servidor o el archivo de script, o si no están protegido en el equipo local, la consola le pide que escriba la contraseña.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Exportar o importar las contraseñas cifradas  
La aplicación de consola de SSMA permite exportar las contraseñas de cifrado de base de datos presentes en un archivo en el equipo local a un archivo protegido y viceversa. Lo ayuda a hacer que la máquina de contraseñas cifradas independientes. Funcionalidad de exportación lee el identificador del servidor y la contraseña de la variable local almacenamiento protegido y guarda la información en un archivo cifrado. El usuario se le pedirá que escriba la contraseña para el archivo protegido. Asegúrese de que la contraseña escrita es la longitud de 8 caracteres o más. Este archivo protegido es portátil entre distintos equipos. Funcionalidad de importación lee al servidor de la información de identificador y la contraseña desde el archivo protegido. El usuario se le pedirá que escriba la contraseña para el archivo protegido y anexa la información en el almacenamiento local protegido.  
  
Ejemplo:  

    Export password
    
    Enter password for protecting the exported file C:\SSMA\SSMAforOracleConsole.EXE -securepassword -export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforOracleConsole.EXE -p -e "OracleDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
Ejemplo:  

    Import an encrypted password
    
    Enter password for protecting the imported file C:\SSMA\SSMAforOracleConsole.EXE -securepassword -import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforOracleConsole.EXE -p -i "OracleDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>Vea también  
[Ejecución de la consola SSMA (Oracle)](https://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
