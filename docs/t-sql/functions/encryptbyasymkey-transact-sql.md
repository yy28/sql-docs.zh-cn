---
title: "ENCRYPTBYASYMKEY (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 711b5887a9411c10c215cc766eb0995c3e056d77
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使用非对称密钥加密数据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>参数  
 *Asym_Key_ID*  
 数据库中非对称密钥的 ID。 **int**。  
  
 *明文形式*  
 将使用非对称密钥加密的数据字符串。  
  
 **@plaintext**  
 是类型的变量**nvarchar**， **char**， **varchar**，**二进制**， **varbinary**，或**nchar**包含要使用非对称密钥加密数据。  
  
## <a name="return-types"></a>返回类型  
 **varbinary** 8000 个字节的最大大小。  
  
## <a name="remarks"></a>注释  
 与使用对称密钥进行加密和解密相比，使用非对称密钥进行加密和解密时的系统开销要高得多。 建议您不要使用非对称密钥加密大型数据集，例如表中的用户数据。 而应该使用强对称密钥加密数据并使用非对称密钥加密对称密钥。  
  
 **EncryptByAsymKey**返回**NULL**如果输入超过一定数量的字节，具体取决于该算法。 限制： 512 位 RSA 密钥可以加密最多 53 个字节，1024 位密钥可以加密达 117 个字节，2048 位密钥可以加密达 245 个字节。 （注意，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，证书和异步密钥都是 RSA 密钥的包装。）  
  
## <a name="examples"></a>示例  
 以下示例将用非对称密钥 `@cleartext` 加密在 `JanainaAsymKey02` 中存储的文本。 加密的数据插入表 `ProtectedData04` 中。  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [DECRYPTBYASYMKEY &#40;Transact SQL &#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

