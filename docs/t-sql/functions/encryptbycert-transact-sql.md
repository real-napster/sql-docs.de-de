---
title: ENCRYPTBYCERT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYCERT
- ENCRYPTBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], encryption
- encryption [SQL Server], certificates
- ENCRYPTBYCERT function
ms.assetid: ab66441f-e2d2-4e3a-bcae-bcc09e12f3c1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 79530fff04d278d9dbc8e1ad1454bc4dca4c885c
ms.sourcegitcommit: b3d84abfa4e2922951430772c9f86dce450e4ed1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/22/2019
ms.locfileid: "56662944"
---
# <a name="encryptbycert-transact-sql"></a>ENCRYPTBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Verschlüsselt Daten mit dem öffentlichen Schlüssel eines Zertifikats.  
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlinksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EncryptByCert ( certificate_ID , { 'cleartext' | @cleartext } )  
```  
  
## <a name="arguments"></a>Argumente  
_certificate\_ID_  
Die ID eines Zertifikats in der Datenbank. **int**.  
  
_Klartext_  
Eine Zeichenfolge mit Daten, die mit dem Zertifikat verschlüsselt werden.  
  
**@cleartext**  
Eine Variable eines der folgenden Typen, die Daten enthalten, die mit dem öffentlichen Schlüssel des Zertifikats verschlüsselt werden:

* **nvarchar** 
* **char**
* **varchar**
* **binary** 
* **varbinary**
* **nchar**
  
## <a name="return-types"></a>Rückgabetypen  
**varbinary** mit einer maximalen Größe von 8.000 Bytes.  
  
## <a name="remarks"></a>Remarks  
Diese Funktion verschlüsselt Daten mit dem öffentlichen Schlüssel des Zertifikats. Der verschlüsselte Text kann nur mit dem entsprechenden privaten Schlüssel entschlüsselt werden. Diese asymmetrischen Transformationen sind im Vergleich zum Verschlüsseln und Entschlüsseln mit einem symmetrischen Schlüssel kostenintensiv. Von der asymmetrischen Verschlüsselung wird daher abgeraten, wenn Sie große Datasets verwenden.
  
## <a name="examples"></a>Beispiele  
In diesem Beispiel wird der in `@cleartext` gespeicherte Nur-Text mit dem Zertifikat mit dem Namen `JanainaCert02` verschlüsselt. Die verschlüsselten Daten werden in die `ProtectedData04`-Tabelle eingefügt.  
  
```  
INSERT INTO [AdventureWorks2012].[ProtectedData04]   
    VALUES ( N'Data encrypted by certificate ''Shipping04''',  
    EncryptByCert(Cert_ID('JanainaCert02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen  
[DECRYPTBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbycert-transact-sql.md)   
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
[ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
[DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
[BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
[Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
