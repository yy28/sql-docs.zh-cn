---
title: "DECRYPTBYASYMKEY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYASYMKEY
- DECRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], DECRYPTBYASYMKEY function
- DECRYPTBYASYMKEY function
- decryption [SQL Server], asymmetric keys
ms.assetid: d9ebcd30-f01c-4cfe-b95e-ffe6ea13788b
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7196e7eedf5d1a808853df55259fcee1891c345
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使用非对称密钥解密数据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
## <a name="arguments"></a>参数  
 *Asym_Key_ID*  
 数据库中非对称密钥的 ID。 *Asym_Key_ID*是**int**。  
  
 *已加密文本*  
 使用非对称密钥加密的数据字符串。  
  
 @ciphertext  
 是类型的变量**varbinary**包含已经用非对称密钥加密的数据。  
  
 *Asym_Key_Password*  
 用于加密数据库中非对称密钥的密码。  
  
## <a name="return-types"></a>返回类型  
 **varbinary** 8000 个字节的最大大小。  
  
## <a name="remarks"></a>注释  
 与使用对称密钥进行加密和解密相比，使用非对称密钥进行加密和解密时的系统开销要高得多。 当处理大型数据集（例如表中的用户数据）时，不推荐使用非对称密钥。  
  
## <a name="permissions"></a>Permissions  
 需要对非对称密钥具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 以下示例将对已使用非对称密钥 `JanainaAsymKey02` 加密的密码进行解密，此非对称密钥存储在 `AdventureWorks2012.ProtectedData04` 中。 返回的数据将使用非对称密钥 `JanainaAsymKey02` 解密，此密钥已使用密码 `pGFD4bb925DGvbd2439587y` 解密。 纯文本转换为类型**nvarchar**。  
  
```  
SELECT CONVERT(nvarchar(max),  
    DecryptByAsymKey( AsymKey_Id('JanainaAsymKey02'),   
    ProtectedData, N'pGFD4bb925DGvbd2439587y' ))   
AS DecryptedData   
FROM [AdventureWorks2012].[Sales].[ProtectedData04]   
WHERE Description = N'encrypted by asym key''JanainaAsymKey02''';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ENCRYPTBYASYMKEY &#40;Transact SQL &#41;](../../t-sql/functions/encryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [选择加密算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

