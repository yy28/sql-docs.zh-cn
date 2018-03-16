---
title: DECRYPTBYKEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DecryptByKey_TSQL
- DECRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], DecryptByKey function
- decryption [SQL Server], keys
- decryption [SQL Server], symmetric keys
- DECRYPTBYKEY function
ms.assetid: 6edf121f-ac62-4dae-90e6-6938f32603c9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a1275be81fdf2a8405d0f744da962c3cf874eea2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="decryptbykey-transact-sql"></a>DECRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使用对称密钥对数据进行解密。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DecryptByKey ( { 'ciphertext' | @ciphertext }   
    [ , add_authenticator, { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>参数  
 *ciphertext*  
 已使用密钥进行加密的数据。 ciphertext 的数据类型为 varbinary。  
  
 **@ciphertext**  
 是 **varbinary** 类型的变量，包含已使用密钥进行加密的数据。  
  
 add_authenticator  
 指示是否与明文一起加密验证器。 对数据进行加密时，该值必须与传递给 EncryptByKey 的值相同。 add_authenticator 的数据类型为 int。  
  
 authenticator  
 用于生成验证器的数据。 必须与提供给 EncryptByKey 的值相匹配。 authenticator 的数据类型为 sysname。  
  
 **@authenticator**  
 包含用于生成验证器的数据的变量。 必须与提供给 EncryptByKey 的值相匹配。  
  
## <a name="return-types"></a>返回类型  
 varbinary（最大大小为 8000 个字节）。  
  
## <a name="remarks"></a>Remarks  
 DecryptByKey 使用对称密钥。 该对称密钥必须已经在数据库中打开。 可以同时打开多个密钥。 不必只在解密密码之前才打开密钥。  
  
 对称加密和解密速度相对较快，适于处理大量数据。  
  
## <a name="permissions"></a>权限  
 需要已在当前会话中打开对称密钥。 有关详细信息，请参阅 [OPEN SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/open-symmetric-key-transact-sql.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-decrypting-by-using-a-symmetric-key"></a>A. 使用对称密钥进行解密  
 以下示例使用对称密钥对密码进行解密。  
  
```  
-- First, open the symmetric key with which to decrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
GO  
  
-- Now list the original ID, the encrypted ID, and the   
-- decrypted ciphertext. If the decryption worked, the original  
-- and the decrypted ID will match.  
SELECT NationalIDNumber, EncryptedNationalID   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalID))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-decrypting-by-using-a-symmetric-key-and-an-authenticating-hash"></a>B. 通过使用对称密钥和验证哈希进行解密  
 以下示例对使用验证器加密的数据进行解密。  
  
```  
-- First, open the symmetric key with which to decrypt the data  
OPEN SYMMETRIC KEY CreditCards_Key11  
   DECRYPTION BY CERTIFICATE Sales09;  
GO  
  
-- Now list the original card number, the encrypted card number,  
-- and the decrypted ciphertext. If the decryption worked,   
-- the original number will match the decrypted number.  
SELECT CardNumber, CardNumber_Encrypted   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByKey(CardNumber_Encrypted, 1 ,   
    HashBytes('SHA1', CONVERT(varbinary, CreditCardID))))   
    AS 'Decrypted card number' FROM Sales.CreditCard;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [ENCRYPTBYKEY (Transact-SQL)](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [选择加密算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
