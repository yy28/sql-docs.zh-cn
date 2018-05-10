---
title: ENCRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYASYMKEY
- ENCRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYASYMKEY function
- encryption [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], ENCRYPTBYASYMKEY function
ms.assetid: 86bb2588-ab13-4db2-8f3c-42c9f572a67b
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 212ce15f0d28b16b81a9c07d785c129b039cdc6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使用非对称密钥加密数据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>参数  
 Asym_Key_ID  
 数据库中非对称密钥的 ID。 int。  
  
 cleartext  
 将使用非对称密钥加密的数据字符串。  
  
 **@plaintext**  
 这是类型为 nvarcharchar varcharbinaryvarbinary 或 nchar 的变量，其中包含要用非对称密钥加密的数据。  
  
## <a name="return-types"></a>返回类型  
 varbinary（最大大小为 8000 个字节）。  
  
## <a name="remarks"></a>Remarks  
 与使用对称密钥进行加密和解密相比，使用非对称密钥进行加密和解密时的系统开销要高得多。 建议您不要使用非对称密钥加密大型数据集，例如表中的用户数据。 而应该使用强对称密钥加密数据并使用非对称密钥加密对称密钥。  
  
 根据算法，如果输入超出一定字节数，**EncryptByAsymKey** 将返回 **NULL**。 限制为：512 位 RSA 密钥可加密达 53 个字节，1024 位密钥可加密达 117 个字节，而 2048 密钥可加密达 245 个字节。 （注意，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，证书和异步密钥都是 RSA 密钥的包装。）  
  
## <a name="examples"></a>示例  
 以下示例将用非对称密钥 `@cleartext` 加密在 `JanainaAsymKey02` 中存储的文本。 加密的数据插入表 `ProtectedData04` 中。  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [DECRYPTBYASYMKEY (Transact-SQL)](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
