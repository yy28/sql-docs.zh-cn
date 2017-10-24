---
title: "DECRYPTBYKEYAUTOASYMKEY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/09/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOASYMKEY_TSQL
- DECRYPTBYKEYAUTOASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOASYMSKEY function
ms.assetid: 5521d4cf-740c-4ede-98b6-4ba90b84e32d
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 74aa8bad7e6d848296ef2997017758883226ac48
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbykeyautoasymkey-transact-sql"></a>DECRYPTBYKEYAUTOASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用对称密钥执行解密，而该对称密钥则使用非对称密钥进行自动解密。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DecryptByKeyAutoAsymKey ( akey_ID , akey_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>参数  
 *akey_ID*  
 用于保护对称密钥的非对称密钥的 ID。 *akey_ID*是**int**。  
  
 *akey_password*  
 用于保护非对称密钥私钥的密码。 如果私钥受数据库主密钥保护，则该值可以为 NULL。 *akey_password*是**nvarchar**。  
  
 *已加密文本*  
 使用密钥进行加密的数据。 *已加密文本*是**varbinary**。  
  
 @ciphertext  
 是类型的变量**varbinary**包含使用密钥加密的数据。  
  
 *add_authenticator*  
 指示是否与明文一起加密验证器。 必须是相同的值传递给 EncryptByKey 时的数据进行加密。 如果使用了验证器，则为 1。 *add_authenticator*是**int**。  
  
 @add_authenticator  
 指示是否与明文一起加密验证器。 必须是相同的值传递给 EncryptByKey 时的数据进行加密。  
  
 *身份验证器*  
 从中生成验证器的数据。 必须与提供给 EncryptByKey 的值相匹配。 *身份验证器*是**sysname**。  
  
 @authenticator  
 包含用于生成验证器的数据的变量。 必须与提供给 EncryptByKey 的值相匹配。  
  
## <a name="return-types"></a>返回类型  
 **varbinary** 8000 个字节的最大大小。  
  
## <a name="remarks"></a>注释  
 DecryptByKeyAutoAsymKey 组合了 OPEN SYMMETRIC KEY 和 DecryptByKey 的功能。 在单个操作中，它对对称密钥进行解密，并使用该密钥来解密已加密文本。  
  
## <a name="permissions"></a>Permissions  
 需要对对称密钥拥有 VIEW DEFINITION 权限以及对非对称密钥拥有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 下例显示如何用 `DecryptByKeyAutoAsymKey` 来简化执行解密的代码。 应在还没有数据库主密钥的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库上运行此代码。  
  
```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE ASYMMETRIC KEY SSN_AKey   
    WITH ALGORITHM = RSA_2048 ;   
GO  
CREATE SYMMETRIC KEY SSN_Key_02 WITH ALGORITHM = DES  
    ENCRYPTION BY ASYMMETRIC KEY SSN_AKey;  
GO  
--  
--Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber2 varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber2  
    = EncryptByKey(Key_GUID('SSN_Key_02'), NationalIDNumber);  
GO  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key.  
--2. Decrypt the data.  
--3. Close the symmetric key.  
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
SELECT NationalIDNumber, EncryptedNationalIDNumber2    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--OPTION TWO, using DecryptByKeyAutoAsymKey()  
SELECT NationalIDNumber, EncryptedNationalIDNumber2   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoAsymKey ( AsymKey_ID('SSN_AKey') , NULL ,EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [OPEN SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact SQL &#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40;Transact SQL &#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

