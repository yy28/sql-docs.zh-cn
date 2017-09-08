---
title: "VERIFYSIGNEDBYCERT (Transact SQL) |Microsoft 文档"
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
- VERIFYSIGNEDBYCERT
- VERIFYSIGNEDBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- digitally signed data for changes [SQL Server]
- verifying digitally signed data for changes
- testing digitally signed data for changes
- checking digitally signed data for changes
- VERIFYSIGNEDBYCERT
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 4e041f33-60c4-4190-91c7-220d51dd6c8f
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6d4725d6e9e28100333040061eafb54f07db9066
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="verifysignedbycert-transact-sql"></a>VERIFYSIGNEDBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  测试经过数字签名的数据在签名后是否发生了更改。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
VerifySignedByCert( Cert_ID , signed_data , signature )  
```  
  
## <a name="arguments"></a>参数  
 *Cert_ID*  
 数据库中证书的 ID。 *Cert_ID*是**int**。  
  
 *signed_data*  
 是类型的变量**nvarchar**， **char**， **varchar**，或**nchar**包含使用证书进行签名的数据。  
  
 *签名*  
 附加到已签名数据中的签名。 *签名*是**varbinary**。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
 如果已签名的数据未更改，则返回 1；否则返回 0。  
  
## <a name="remarks"></a>注释  
 **VerifySignedBycert**通过使用指定的证书的公钥解密的数据和数据的新计算 MD5 哈希处理的解密的值进行比较。 如果值匹配，则确认签名有效。  
  
## <a name="permissions"></a>Permissions  
 需要对证书拥有 VIEW DEFINITION 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-verifying-that-signed-data-has-not-been-tampered-with"></a>A. 验证已签名的数据尚未被篡改  
 以下示例测试 `Signed_Data` 中的信息是否自使用名为 `Shipping04` 的证书对其进行签名之后发生了更改。 签名存储在 `DataSignature` 中。 证书 `Shipping04` 将传递给 `Cert_ID`，后者则返回数据库中证书的 ID。 如果 `VerifySignedByCert` 返回 1，则表示签名正确。 如果 `VerifySignedByCert` 返回 0，则 `Signed_Data` 中的数据不是用于生成 `DataSignature` 的数据。 在这种情况下，要么 `Signed_Data` 自签名以来发生了更改，要么 `Signed_Data` 使用不同的证书进行了签名。  
  
```  
SELECT Data, VerifySignedByCert( Cert_Id( 'Shipping04' ),  
    Signed_Data, DataSignature ) AS IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
### <a name="b-returning-only-records-that-have-a-valid-signature"></a>B. 仅返回包含有效签名的记录  
 此查询仅返回自使用证书 `Shipping04` 签名以来尚未更改的记录。  
  
```  
SELECT Data FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByCert( Cert_Id( 'Shipping04' ), Data,   
    DataSignature ) = 1   
AND Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CERT_ID &#40;Transact SQL &#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [SIGNBYCERT &#40;Transact SQL &#41;](../../t-sql/functions/signbycert-transact-sql.md)   
 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [删除证书 &#40;Transact SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE (Transact-SQL)](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
