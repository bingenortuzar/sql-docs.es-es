---
title: Métodos de OGC en instancias de geometry | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- OGC Methods on Geometry Instances [SQL Server]
ms.assetid: c0c0f441-bf33-410c-9df0-544e3d05b944
author: MladjoA
ms.author: mlandzic
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f0d6cce8e9476711b1abfced08559f74ee9c6f0a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101115"
---
# <a name="ogc-methods-on-geometry-instances"></a>Métodos de OGC en instancias de geometry
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite los métodos de Open Geospatial Consortium (OGC) en las instancias de Geometry.  
  
 Para obtener más información acerca de las especificaciones de OGC, vea lo siguiente:  
  
-   [Especificaciones de OGC, Acceso a características simples, Parte 1 - Arquitectura común](https://go.microsoft.com/fwlink/?LinkId=93627)  
  
-   [Especificaciones de OGC, acceso a características simples, parte 2: opciones de SQL](https://go.microsoft.com/fwlink/?LinkId=93628)  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [STArea](../../t-sql/spatial-geometry/starea-geometry-data-type.md)  
  
-   [STAsBinary](../../t-sql/spatial-geometry/stasbinary-geometry-data-type.md)  
  
-   [STAsText](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)  
  
-   [STBoundary](../../t-sql/spatial-geometry/stboundary-geometry-data-type.md)  
  
-   [STBuffer](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)  
  
-   [STCentroid](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)  
  
-   [STContains](../../t-sql/spatial-geometry/stcontains-geometry-data-type.md)  
  
-   [STConvexHull](../../t-sql/spatial-geometry/stconvexhull-geometry-data-type.md)  
  
-   [STCrosses](../../t-sql/spatial-geometry/stcrosses-geometry-data-type.md)  
  
-   [STCurveN &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stcurven-geometry-data-type.md)  
  
-   [STCurveToLine &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stcurvetoline-geometry-data-type.md)  
  
-   [STDifference](../../t-sql/spatial-geometry/stdifference-geometry-data-type.md)  
  
-   [STDimension](../../t-sql/spatial-geometry/stdimension-geometry-data-type.md)  
  
-   [STDisjoint](../../t-sql/spatial-geometry/stdisjoint-geometry-data-type.md)  
  
-   [STDistance](../../t-sql/spatial-geometry/stdistance-geometry-data-type.md)  
  
-   [STEndpoint](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)  
  
-   [STEnvelope](../../t-sql/spatial-geometry/stenvelope-geometry-data-type.md)  
  
-   [STEquals](../../t-sql/spatial-geometry/stequals-geometry-data-type.md)  
  
-   [STExteriorRing](../../t-sql/spatial-geometry/stexteriorring-geometry-data-type.md)  
  
-   [STGeometryN](../../t-sql/spatial-geometry/stgeometryn-geometry-data-type.md)  
  
-   [STGeometryType](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
-   [STInteriorRingN](../../t-sql/spatial-geometry/stinteriorringn-geometry-data-type.md)  
  
-   [STIntersection](../../t-sql/spatial-geometry/stintersection-geometry-data-type.md)  
  
-   [STIntersects](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
-   [STIsClosed](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)  
  
-   [STIsEmpty](../../t-sql/spatial-geometry/stisempty-geometry-data-type.md)  
  
-   [STIsRing](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)  
  
-   [STIsSimple](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md)  
  
-   [STIsValid](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
-   [STLength](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)  
  
-   [STNumCurves &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)  
  
-   [STNumGeometries](../../t-sql/spatial-geometry/stnumgeometries-geometry-data-type.md)  
  
-   [STNumInteriorRing](../../t-sql/spatial-geometry/stnuminteriorring-geometry-data-type.md)  
  
-   [STNumPoints](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)  
  
-   [STOverlaps](../../t-sql/spatial-geometry/stoverlaps-geometry-data-type.md)  
  
-   [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)  
  
-   [STPointOnSurface](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)  
  
-   [STRelate](../../t-sql/spatial-geometry/strelate-geometry-data-type.md)  
  
-   [STSrid](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)  
  
-   [STStartPoint](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)  
  
-   [STSymDifference](../../t-sql/spatial-geometry/stsymdifference-geometry-data-type.md)  
  
-   [STTouches](../../t-sql/spatial-geometry/sttouches-geometry-data-type.md)  
  
-   [STUnion](../../t-sql/spatial-geometry/stunion-geometry-data-type.md)  
  
-   [STWithin](../../t-sql/spatial-geometry/stwithin-geometry-data-type.md)  
  
-   [STX](../../t-sql/spatial-geometry/stx-geometry-data-type.md)  
  
-   [STY](../../t-sql/spatial-geometry/sty-geometry-data-type.md)  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Métodos de geometría estáticos de OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)   
 [Métodos de geometría estáticos ampliados](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  
