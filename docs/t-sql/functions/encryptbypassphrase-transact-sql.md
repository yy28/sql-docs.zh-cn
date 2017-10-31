---
title: "ENCRYPTBYPASSPHRASE (Transact SQL) |Microsoft 文档"
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
- ENCRYPTBYPASSPHRASE
- ENCRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYPASSPHRASE function
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYPASSPHRASE function
ms.assetid: f8dbb9e6-94d6-40d7-8b38-6833a409d597
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ddfbea4ac550f21787eb88db6119c391f2b1b85a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="encryptbypassphrase-transact-sql"></a>ENCRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  通过使用 TRIPLE DES 算法以及 128 密钥位长度的通行短语对数据加密。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
EncryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'cleartext' | @cleartext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>参数  
 *通行短语*  
 用于生成对称密钥的通行短语。  
  
 @passphrase  
 类型的变量的**nvarchar**， **char**， **varchar**，**二进制**， **varbinary**，或**nchar**包含从其生成对称密钥的通行短语。  
  
 *明文形式*  
 要加密的明文。  
  
 @cleartext  
 类型的变量的**nvarchar**， **char**， **varchar**，**二进制**， **varbinary**，或**nchar**包含明文形式。 最大大小为 8000 个字节。  
  
 *add_authenticator*  
 指示是否将验证器与明文一起加密。 如果将添加验证器，则为 1。 **int**。  
  
 @add_authenticator  
 指示是否将哈希与明文一起加密。  
  
 *身份验证器*  
 用于派生验证器的数据。 **sysname**。  
  
 @authenticator  
 包含验证器所源自的数据的变量。  
  
## <a name="return-types"></a>返回类型  
 **varbinary**为 8000 个字节的最大大小。  
  
## <a name="remarks"></a>注释  
 通行短语是包含空格的密码。 使用通行短语的优点在于，与相对较长的字符串相比，有含义的短语或句子更容易记忆。  
  
 此函数不检查密码复杂性。  
  
## <a name="examples"></a>示例  
 以下示例将更新 `SalesCreditCard` 表中的记录，并使用主键作为验证器来加密存储在 `CardNumber_EncryptedbyPassphrase` 列中的信用卡号的值。  
  
```  
USE AdventureWorks2012;  
GO  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard   
    ADD CardNumber_EncryptedbyPassphrase varbinary(256);   
GO  
-- First get the passphrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
    = 'A little learning is a dangerous thing!';  
  
-- Update the record for the user's credit card.  
-- In this case, the record is number 3681.  
UPDATE Sales.CreditCard  
SET CardNumber_EncryptedbyPassphrase = EncryptByPassPhrase(@PassphraseEnteredByUser  
    , CardNumber, 1, CONVERT( varbinary, CreditCardID))  
WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [DECRYPTBYPASSPHRASE &#40;Transact SQL &#41;](../../t-sql/functions/decryptbypassphrase-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

