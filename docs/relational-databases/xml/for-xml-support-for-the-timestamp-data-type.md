---
title: FOR XML-Unterstützung für den timestamp-Datentyp | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type
ms.assetid: 4e1920e1-e7a4-4069-965e-3f6039a6099e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3cf28d43ac3eb55d0377d0ec25be66db6abfaca
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510237"
---
# <a name="for-xml-support-for-the-timestamp-data-type"></a>FOR XML-Unterstützung für den timestamp-Datentyp
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  In der FOR XML-Transformation werden **timestamp** -Typwerte als **varbinary(8)** -Daten behandelt und sind immer Base-64-codiert. Das XSD- oder XDR-Schema gibt, falls angefordert, diesen Typ wieder.  
  
```  
drop table t  
go  
create table t  
(c1 int,  
 c2 timestamp)  
go  
  
insert t values(1, null)  
go  
select * from t  
for xml auto, xmldata  
go  
```  
  
 Dies ist das Ergebnis:  
  
```  
<Schema name="Schema1"   
        xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes">  
  <ElementType name="t" content="empty" model="closed">  
    <AttributeType name="c1" dt:type="i4" />  
    <AttributeType name="c2" dt:type="bin.base64" />  
    <attribute type="c1" />  
    <attribute type="c2" />  
  </ElementType>  
</Schema>  
<t xmlns="x-schema:#Schema1" c1="1" c2="AAAAAAAAH04=" />  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [FOR XML-Unterstützung für verschiedene SQL Server-Datentypen](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
