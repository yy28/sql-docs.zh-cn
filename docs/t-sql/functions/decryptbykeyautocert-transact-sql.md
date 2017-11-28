---
title: "DECRYPTBYKEYAUTOCERT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/09/2015
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOCERT
- DECRYPTBYKEYAUTOCERT_TSQL
dev_langs: TSQL
helpviewer_keywords: DECRYPTBYKEYAUTOCERT function
ms.assetid: 6b45fa2e-ffaa-46f7-86ff-5624596eda4a
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9aca90f988ae2d12d9a7c26f01673530b1a07f4b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="decryptbykeyautocert-transact-sql"></a>DECRYPTBYKEYAUTOCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用通过证书自动解密的对称密钥进行解密。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DecryptByKeyAutoCert ( cert_ID , cert_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>参数  
 *cert_ID*  
 用于保护对称密钥的证书的 ID。 *cert_ID*是**int**。  
  
 *cert_password*  
 用于保护证书私钥的密码。 如果私钥受数据库主密钥保护，则该值可以为 NULL。 *cert_password*是**nvarchar**。  
  
 *已加密文本*  
 使用密钥进行加密的数据。 *已加密文本*是**varbinary**。  
  
 @ciphertext  
 是类型的变量**varbinary**包含使用密钥加密的数据。  
  
 *add_authenticator*  
 指示是否与明文一起加密验证器。 必须是相同的值传递给 EncryptByKey 时的数据进行加密。是**1**如果使用验证器。 *add_authenticator*是**int**。  
  
 @add_authenticator  
 指示是否与明文一起加密验证器。 必须是相同的值传递给 EncryptByKey 时的数据进行加密。  
  
 *身份验证器*  
 从中生成验证器的数据。 必须与提供给 EncryptByKey 的值相匹配。 *身份验证器*是**sysname**。  
  
 @authenticator  
 包含用于生成验证器的数据的变量。 必须与提供给 EncryptByKey 的值相匹配。  
  
## <a name="return-types"></a>返回类型  
 **varbinary** 8000 个字节的最大大小。  
  
## <a name="remarks"></a>注释  
 DecryptByKeyAutoCert 组合了 OPEN SYMMETRIC KEY 和 DecryptByKey 的功能。 在单个操作中，它可以解密对称密钥，并使用该密钥解密密码文本。  
  
## <a name="permissions"></a>Permissions  
 需要对对称密钥拥有 VIEW DEFINITION 权限以及对证书拥有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 下例显示如何用 `DecryptByKeyAutoCert` 来简化执行解密的代码。 应在还没有数据库主密钥的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库上运行此代码。  
  
```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE CERTIFICATE HumanResources037   
   WITH SUBJECT = 'Sammamish HR',   
   EXPIRY_DATE = '10/31/2009';  
CREATE SYMMETRIC KEY SSN_Key_01 WITH ALGORITHM = DES  
    ENCRYPTION BY CERTIFICATE HumanResources037;  
GO  
----Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037 ;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
--  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key  
--2. Decrypt the data  
--3. Close the symmetric key  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
SELECT NationalIDNumber, EncryptedNationalIDNumber    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--OPTION TWO, using DecryptByKeyAutoCert()  
SELECT NationalIDNumber, EncryptedNationalIDNumber   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoCert ( cert_ID('HumanResources037') , NULL ,EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
```  
  
## <a name="see-also"></a>另请参阅  
 [OPEN SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact SQL &#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40;Transact SQL &#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
