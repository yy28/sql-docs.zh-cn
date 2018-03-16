---
title: SIGNBYASYMKEY (Transact-SQL) | Microsoft Docs
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
- SIGNBYASYMKEY_TSQL
- SIGNBYASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- text signing [SQL Server]
- encryption [SQL Server], asymmetric keys
- signing text [SQL Server]
- SIGNBYASYMKEY function
- asymmetric keys [SQL Server], SIGNBYASYMKEY function
- cryptography [SQL Server], asymmetric keys
- clear text signing
ms.assetid: b1c46159-cc76-4205-a841-8f4a71742f80
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd32b46481866acb59c7c94a18a66507171fb36c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="signbyasymkey-transact-sql"></a>SIGNBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使用非对称密钥签署纯文本  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SignByAsymKey( Asym_Key_ID , @plaintext [ , 'password' ] )  
```  
  
## <a name="arguments"></a>参数  
 Asym_Key_ID  
 当前数据库中非对称密钥的 ID。 Asym_Key_ID 的数据类型为 int。  
  
 **@plaintext**  
 类型为 nvarchar、char、varchar 或 nchar 的变量，其中包含将使用非对称密钥进行签名的数据。  
  
 password  
 用于保护私钥的密码。 password 的数据类型为 nvarchar(128)。  
  
## <a name="return-types"></a>返回类型  
 varbinary（最大大小为 8000 个字节）。  
  
## <a name="remarks"></a>Remarks  
 需要对非对称密钥具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 以下示例创建表 `SignedData04`，该表用于存储纯文本和它的签名。 然后，它在表中插入以非对称密钥 `PrimeKey` 签署的记录，该密钥首先以密码 `'pGFD4bb925DGvbd2439587y'` 进行解密。  
  
```  
-- Create a table in which to store the data  
CREATE TABLE [SignedData04](Description nvarchar(max), Data nvarchar(max), DataSignature varbinary(8000));  
GO  
-- Store data together with its signature  
DECLARE @clear_text_data nvarchar(max);  
set @clear_text_data = N'Important numbers 2, 3, 5, 7, 11, 13, 17,   
      19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79,  
      83, 89, 97';  
INSERT INTO [SignedData04]   
    VALUES( N'data encrypted by asymmetric key ''PrimeKey''',  
    @clear_text_data, SignByAsymKey( AsymKey_Id( 'PrimeKey' ),  
    @clear_text_data, N'pGFD4bb925DGvbd2439587y' ));  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ASYMKEY_ID (Transact-SQL)](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [VERIFYSIGNEDBYASYMKEY (Transact-SQL)](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
