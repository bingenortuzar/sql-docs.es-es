---
title: Cuadro de diálogo Advertencias de validación (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65556
- vdt.dlgbox.validationwarnings
ms.assetid: fc76e234-ec9c-4a19-a65b-cb558ec8268e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: eb7dc987ba03dc4d50c12c80519f769d6f5b3261
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267448"
---
# <a name="validation-warnings-dialog-box-visual-database-tools"></a>Advertencias de validación (cuadro de diálogo, Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Este cuadro de diálogo aparece si intenta guardar modificaciones que pueden producir efectos secundarios malintencionados o si es probable que se produzca un error en la operación de confirmación de la base de datos. Este cuadro de diálogo indica en qué pueden consistir estos efectos secundarios o por qué podría producirse un error en la operación de confirmación. Proporciona la opción de seguir con la modificación o cancelar la operación.  
  
> [!NOTE]  
> Este cuadro de diálogo aparece al intentar transferir las modificaciones realizadas a la base de datos o al guardar un script de cambio.  
  
El cuadro de diálogo puede aparecer por cualquiera de estos motivos:  
  
-   Puede que no tenga permisos en la base de datos para confirmar todas las modificaciones.  
  
-   Las modificaciones podrían producir restricciones CHECK, restricciones DEFAULT o columnas derivadas incorrectamente formadas.  
  
-   Una modificación del tipo de datos de una columna podría ocasionar una pérdida de datos.  
  
-   Una modificación podría producir un índice de más de 900 bytes.  
  
-   Una modificación podría cambiar una tabla o columna que contribuye a una vista enlazada a un esquema o a una función definida por el usuario.  
  
-   Una modificación podría hacer que se volviera a generar una tabla con uno o más desencadenadores cifrados; se quitarán los desencadenadores.  
  
-   Las modificaciones producirían una configuración inusual de ANSI_NULLS o ANSI_PADDING, o ambos en las columnas de una tabla.  
  
## <a name="options"></a>Opciones  
**Sí**  
Se continua la operación para generar el script de cambio o transferir las modificaciones a la base de datos. La operación de confirmación puede generar errores si no tiene privilegios para modificar la base de datos, si las modificaciones realizadas producen un índice de más de 900 bytes o si dan lugar a restricciones CHECK, restricciones DEFAULT o columnas calculadas incorrectamente formadas.  
  
**No**  
Cancela la acción de guardar.  
  
**Guardar archivo de texto**  
Muestra el cuadro de diálogo **Guardar como** , que permite especificar una ubicación para un archivo de texto que contiene una lista de advertencias.  
  
## <a name="see-also"></a>Consulte también  
[Diseñar tablas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
