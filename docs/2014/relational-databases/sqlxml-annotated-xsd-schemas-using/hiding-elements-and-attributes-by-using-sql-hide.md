---
title: 'Ausblenden von Elementen und Attributen mit SQL: Hide | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- hiding elements
- element mapping [SQLXML], hiding attributes and elements
- hide annotation
- sql:hide
- table/view mapping [SQLXML], hiding attributes and elements
- table mapping [SQLXML], hiding attributes and elements
- hiding attributes
- annotated XSD schemas, hiding attributes and elements
- attribute mapping [SQLXML], hiding attributes and elements
- column mapping [SQLXML]
- element hiding [SQLXML]
- XSD schemas [SQLXML], hiding attributes and elements
- attribute hiding [SQLXML]
ms.assetid: 0978301b-f068-46b6-82b9-dc555161f52e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 541f5ccff727552730e4648552ad5126fdfd4858
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2018
ms.locfileid: "52793612"
---
# <a name="hiding-elements-and-attributes-by-using-sqlhide"></a>Ausblenden von Elementen und Attributen mit sql:hide
  Wenn eine XPath-Abfrage mit einem XSD-Schema ausgeführt wird, verfügt das resultierende XML-Dokument über Elemente und Attribute, die im Schema angegeben sind. Sie können mit der `sql:hide`-Anmerkung angeben, dass Elemente und Attribute im Schema ausgeblendet werden sollen. Dies ist hilfreich, wenn das Auswahlkriterium der Abfrage bestimmte Elemente oder Attribute im Schema erfordert, diese jedoch nicht im generierten XML-Dokument zurückgegeben werden sollen.  
  
 Die `sql:hide`-Anmerkung akzeptiert einen booleschen Wert (0 = false, 1 = true). Zulässig sind die Werte 0, 1, true und false.  
  
## <a name="examples"></a>Beispiele  
 Es müssen bestimmte Anforderungen erfüllt sein, damit aus den folgenden Beispielen funktionierende Beispiele erstellt werden können. Weitere Informationen finden Sie unter [Anforderungen für die Ausführung von SQLXML-Beispielen](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqlhide-on-an-attribute"></a>A. Angeben von sql:hide für ein Attribut  
 Das XSD-Schema in diesem Beispiel besteht aus einem  **\<Person.Contact >** -Element mit **ContactID**, **FirstName**, und **"LastName"** Attribute.  
  
 Die  **\<Person.Contact >** -Element komplexen Typs ist, und wird aus diesem Grund wird der Tabelle mit dem gleichen Namen (standardzuordnung). Alle Attribute des  **\<Person.Contact >** Element sind vom einfachen Typ und Spalten mit den gleichen Namen in der Person.Contacttable in der AdventureWorks-Datenbank. Im Schema die `sql:hide` -Anmerkung für das **ContactID** Attribut. Wenn eine XPath-Abfrage mit diesem Schema wird die **ContactID** in das XML-Dokument nicht zurückgegeben wird.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID"  sql:hide="true" />   
       <xsd:attribute name="FirstName"   type="xsd:string" />   
       <xsd:attribute name="LastName"    type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>So testen Sie eine Beispiel-XPath-Abfrage anhand des Schemas  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen Hide.xml.  
  
2.  Kopieren Sie die folgende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen HideT.xml in dem Verzeichnis, in dem Sie zuvor Hide.xml gespeichert haben.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="Hide.xml">  
            /Person.Contact[@ContactID="1"]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungschema (Hide.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\Hide.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [Verwenden von ADO zum Ausführen von SQLXML 4.0-Abfragen](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <Person.Contact FirstName="Gustavo" LastName="Achong" />   
</ROOT>  
```  
  
 Wenn `sql:hide` für ein Element angegeben wird, werden das betreffende Element und dessen Attribute oder untergeordneten Elemente nicht im generierten XML-Dokument ausgegeben. Hier ist ein anderes XSD-Schema in der `sql:hide` angegeben ist, auf die  **\<OD >** Element:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:annotation>  
    <xsd:documentation>  
      Sales.Customer-Sales.SalesOrderHeader-Sales.SalesOrderDetail Schema  
      Copyright 2004 Microsoft. All rights reserved.  
    </xsd:documentation>  
    <xsd:appinfo>  
      <sql:relationship name="CustomerOrder"  
         parent="Sales.Customer"  
                  parent-key="CustomerID"  
                  child-key="CustomerID"  
                  child="Sales.SalesOrderHeader" />  
       <sql:relationship name="OrderOrderDetails"  
                  parent="Sales.SalesOrderHeader"  
                  parent-key="SalesOrderID"  
                  child-key="SalesOrderID"  
                  child="Sales.SalesOrderDetail"/>  
    </xsd:appinfo>  
  </xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Sales.Customer">  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"   
                     maxOccurs="unbounded"   
                     sql:relationship="CustomerOrder">  
          <xsd:complexType>  
            <xsd:sequence>  
               <xsd:element name="OD" sql:relation="Sales.SalesOrderDetail"                                       maxOccurs="unbounded"                                       sql:relationship="OrderOrderDetails"                                       sql:hide="1">  
                  <xsd:complexType>  
                    <xsd:attribute name="SalesOrderID" type="xsd:string"/>  
                    <xsd:attribute name="ProductID" type="xsd:string"/>  
                  </xsd:complexType>  
               </xsd:element>  
            </xsd:sequence>  
          <xsd:attribute name="CustomerID" type="xsd:string"/>  
          <xsd:attribute name="OID" sql:field="SalesOrderID"   
                                    type="xsd:string"/>  
          <xsd:attribute name="OrderDate" type="xsd:date"/>   
        </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
    <xsd:attribute name="CID" sql:field="CustomerID"   
                                type="xsd:string"/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Wenn eine XPath-Abfrage (z. B. `/Customers[@CID="1"]`) angegeben für dieses Schema, das XML-Dokument, das generiert wird, enthält keine der  **\<OD >** Element und seine untergeordneten Elemente, wie im folgenden Teilergebnis gezeigt:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customers CID="1">  
    <Order CustomerID="1" OID="43860" OrderDate="2001-08-01" />   
    <Order CustomerID="1" OID="44501" OrderDate="2001-11-01" />   
    <Order CustomerID="1" OID="45283" OrderDate="2002-02-01" />   
    <Order CustomerID="1" OID="46042" OrderDate="2002-05-01" />   
  </Customers>  
</ROOT>  
```  
  
  
