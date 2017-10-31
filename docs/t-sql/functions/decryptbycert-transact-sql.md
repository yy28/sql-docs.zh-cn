---
title: "DECRYPTBYCERT (Transact SQL) |Microsoft 文档"
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
- DecryptByCert_TSQL
- DECRYPTBYCERT
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], decryption
- decryption [SQL Server], certificates
- DECRYPTBYCERT function
ms.assetid: 4950d787-40fa-4e26-bce8-2cb2ceca12fb
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ebdc328e49635af823cd64e8539ee5b7cfa95c76
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbycert-transact-sql"></a>DECRYPTBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  用证书的私钥解密数据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DecryptByCert ( certificate_ID , { 'ciphertext' | @ciphertext }   
    [ , { 'cert_password' | @cert_password } ] )  
```  
  
## <a name="arguments"></a>参数  
 *certificate_ID*  
 数据库中证书的 ID。 *证书*_ID 是**int**。  
  
 *已加密文本*  
 已用证书的公钥加密的数据的字符串。  
  
 @ciphertext  
 是类型的变量**varbinary**包含已使用证书加密的数据。  
  
 *cert_password*  
 用来加密证书私钥的密码。 必须为 Unicode 字符。  
  
 @cert_password  
 是类型的变量**nchar**或**nvarchar**包含用于加密证书的私钥的密码。 必须为 Unicode 字符。  
  
## <a name="return-types"></a>返回类型  
 **varbinary** 8000 个字节的最大大小。  
  
## <a name="remarks"></a>注释  
 此函数用证书的私钥解密数据。 使用非对称密钥进行的加密转换会消耗大量资源。 因此，EncryptByCert 和 DecryptByCert 不适合用于对用户数据的例行加密。  
  
## <a name="permissions"></a>Permissions  
 需要对证书具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 下面的示例从 `[AdventureWorks2012].[ProtectedData04]` 中选择标记为 `data encrypted by certificate JanainaCert02` 的行。 此示例使用证书 `JanainaCert02` 的私钥对密码进行解密，首次解密时使用的是证书的密码 `pGFD4bb925DGvbd2439587y`。 已解密的数据转换从**varbinary**到**nvarchar**。  
  
```  
SELECT convert(nvarchar(max), DecryptByCert(Cert_Id('JanainaCert02'),  
    ProtectedData, N'pGFD4bb925DGvbd2439587y'))  
FROM [AdventureWorks2012].[ProtectedData04]   
WHERE Description   
    = N'data encrypted by certificate '' JanainaCert02''';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ENCRYPTBYCERT &#40;Transact SQL &#41;](../../t-sql/functions/encryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [删除证书 &#40;Transact SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE (Transact-SQL)](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

