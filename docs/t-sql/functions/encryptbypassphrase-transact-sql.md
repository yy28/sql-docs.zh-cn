---
title: ENCRYPTBYPASSPHRASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8aefacd470b045caafc73474126468fc01658276
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904367"
---
# <a name="encryptbypassphrase-transact-sql"></a>ENCRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
 passphrase   
 用于生成对称密钥的通行短语。  
  
 @passphrase  
 类型为 nvarchar、char、varchar、binary、varbinary 或 nchar 的变量，其中包含用于生成对称密钥的通行短语       。  
  
 cleartext   
 要加密的明文。  
  
 @cleartext  
 类型为 nvarchar、char、varchar、binary、varbinary 或 nchar 的变量，其中包含明文       。 最大大小为 8000 个字节。  
  
 add_authenticator   
 指示是否将验证器与明文一起加密。 如果将添加验证器，则为 1。 int  。  
  
 @add_authenticator  
 指示是否将哈希与明文一起加密。  
  
 authenticator   
 用于派生验证器的数据。 sysname  。  
  
 @authenticator  
 包含验证器所源自的数据的变量。  
  
## <a name="return-types"></a>返回类型  
 varbinary（最大大小为 8000 个字节）  。  
  
## <a name="remarks"></a>Remarks  
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
 [DECRYPTBYPASSPHRASE (Transact-SQL)](../../t-sql/functions/decryptbypassphrase-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
