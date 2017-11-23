---
title: "VERIFYSIGNEDBYASYMKEY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VERIFYSIGNEDBYASYMKEY_TSQL
- VERIFYSIGNEDBYASYMKEY
dev_langs: TSQL
helpviewer_keywords:
- verifying digitally signed data for changes
- VERIFYSIGNEDBYASYMKEY
- testing digitally signed data for changes
- checking digitally signed data for changes
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 9f7c6e0b-5ba4-4dbb-994d-5bd59f4908de
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88e18f3f2eee5d77e450f7529336cc134f52ed44
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="verifysignedbyasymkey-transact-sql"></a>VERIFYSIGNEDBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  测试经过数字签名的数据在签名后是否发生了更改。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
VerifySignedByAsymKey( Asym_Key_ID , clear_text , signature )  
```  
  
## <a name="arguments"></a>参数  
 *Asym_Key_ID*  
 数据库中非对称密钥证书的 ID。  
  
 *clear_text*  
 正在验证的明文数据。  
  
 *签名*  
 附加到已签名数据中的签名。 *签名*是**varbinary**。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
 如果签名匹配，则返回 1；否则返回 0。  
  
## <a name="remarks"></a>注释  
 **VerifySignedByAsymKey**通过使用指定的非对称密钥的公钥解密的数据和数据的新计算 MD5 哈希处理的解密的值进行比较。 如果值匹配，则确认签名有效。  
  
## <a name="permissions"></a>Permissions  
 要求对非对称密钥具有 VIEW DEFINITION 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-testing-for-data-with-a-valid-signature"></a>A. 测试具有有效签名的数据  
 如果所选数据在使用 `WillisKey74` 非对称密钥进行签名后未曾更改，则以下示例返回 1。 如果数据已被篡改，则该示例返回 0。  
  
```  
SELECT Data,  
     VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), SignedData,  
     DataSignature ) as IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
RETURN;  
```  
  
### <a name="b-returning-a-result-set-that-contains-data-with-a-valid-signature"></a>B. 返回包含带有有效签名数据的结果集  
 如果 `SignedData04` 所包含的数据在使用 `WillisKey74` 非对称密钥进行签名后未曾更改，则以下示例返回 SignedData04 中的行。 该示例调用 `AsymKey_ID` 函数从数据库中获取非对称密钥 ID。  
  
```  
SELECT Data   
FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), Data,  
     DataSignature ) = 1  
AND Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ASYMKEY_ID &#40;Transact SQL &#41;](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [SIGNBYASYMKEY &#40;Transact SQL &#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY (Transact-SQL)](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
