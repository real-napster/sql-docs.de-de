---
title: InstanceOf (geometry-Datentyp) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d093331425443a0879d5f59f5a2d03fdebcb2abd
ms.sourcegitcommit: ad3b2133585bc14fc6ef8be91f8b74ee2f498b64
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2019
ms.locfileid: "56425755"
---
# <a name="instanceof-geometry-data-type"></a>InstanceOf (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Eine Methode, die die Übereinstimmung der **geometry**-Instanz mit dem angegebenen Typ überprüft. Gibt „1“ zurück, wenn der Typ einer **geometry**-Instanz dem angegebenen Typ entspricht. Diese Methode gibt auch „1“ zurück, wenn der angegebene Typ ein Vorgänger des Instanztyps ist. Andernfalls gibt diese Methode den Wert „0“ zurück.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.InstanceOf (geometry_type )  
```  
  
## <a name="arguments"></a>Argumente  
*geometry_type*  
Eine **nvarchar(4000)**-Zeichenfolge, die einen von 15 Typen angibt, die in der **geometry**-Typhierarchie verfügbar gemacht werden.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 Die Eingabe für die Methode muss einem der folgenden Typen entsprechen: **Geometry**, **Point**, **Curve**, **LineString**, **CircularString**, **CompoundCurve**, **Surface**, **Polygon**, **CurvePolygon**, **GeometryCollection**, **MultiSurface**, **MultiPolygon**, **MultiCurve**, **MultiLineString** oder **MultiPoint**. Diese Methode löst eine **ArgumentException** aus, wenn andere Zeichenfolgen für die Eingabe verwendet werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `MultiPoint`-Instanz erstellt und `InstanceOf()` verwendet, um zu überprüfen, ob die Instanz eine `GeometryCollection` ist.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [Erweiterte Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

