---
title: "DECRYPTBYPASSPHRASE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYPASSPHRASE
- DECRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], DECRYPTBYPASSPHRASE function
- DECRYPTBYPASSPHRASE function
ms.assetid: ca34b5cd-07b3-4dca-b66a-ed8c6a826c95
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0af2f19acced57d722427c8f341db62dbdb34198
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbypassphrase-transact-sql"></a>DECRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  对使用通行短语加密的数据进行解密。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DecryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>参数  
 *通行短语*  
 将用于生成解密密钥的通行短语。  
  
 @passphrase  
 是类型的变量**nvarchar**， **char**， **varchar**，或**nchar**包含将用于生成的密钥的密码解密。  
  
 *已加密文本*  
 要解密的加密文本。  
  
 @ciphertext  
 是类型的变量**varbinary** ，其中包含已加密文本。 最大大小为 8,000 个字节。  
  
 *add_authenticator*  
 指示是否与明文一起加密验证器。 如果使用了验证器，则为 1。 **int**。  
  
 @add_authenticator  
 指示是否与明文一起加密验证器。 如果使用了验证器，则为 1。 **int**。  
  
 *身份验证器*  
 这是验证器数据。 **sysname**。  
  
 @authenticator  
 包含用于派生验证器的数据的变量。  
  
## <a name="return-types"></a>返回类型  
 **varbinary** 8000 个字节的最大大小。  
  
## <a name="remarks"></a>注释  
 执行该函数无需任何权限。  
  
 如果使用了错误的通行短语或验证器信息，则返回 NULL。  
  
 该通行短语用于生成一个解密密钥，该密钥不会持久化。  
  
 如果对加密文本进行解密时包括验证器，则必须在解密时提供该验证器。 如果解密时提供的验证器值与使用数据加密的验证器值不匹配，则解密将失败。  
  
## <a name="examples"></a>示例  
 下面的示例解密中更新的记录[EncryptByPassPhrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md)。  
  
```  
USE AdventureWorks2012;  
-- Get the pass phrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
= 'A little learning is a dangerous thing!';  
  
-- Decrypt the encrypted record.  
SELECT CardNumber, CardNumber_EncryptedbyPassphrase   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByPassphrase(@PassphraseEnteredByUser, CardNumber_EncryptedbyPassphrase, 1   
    , CONVERT(varbinary, CreditCardID)))  
    AS 'Decrypted card number' FROM Sales.CreditCard   
    WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [选择加密算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ENCRYPTBYPASSPHRASE (Transact-SQL)](../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
  
  

