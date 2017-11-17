---
title: "CERTPRIVATEKEY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
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
- CERTPRIVATEKEY
- CERTPRIVATEKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTPRIVATEKEY
ms.assetid: 33e0f01e-39ac-46da-94ff-fe53b1116df4
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 11a44f9203f9242a8f90ce3ca667bc1fea479dc2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="certprivatekey-transact-sql"></a>CERTPRIVATEKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

返回二进制格式的证书私钥。 此函数有三个参数。
-   一个证书 ID。  
-   一个加密密码，用于对该函数返回的私钥位加密，防止密钥以明文形式向用户公开。  
-   一个可选的解密密码。 如果指定了解密密码，则用它来对证书的私钥解密，否则使用数据库主密钥。  
  
只有有权访问证书私钥的用户才能使用此函数。 此函数返回 PVK 格式的私钥。
  
## <a name="syntax"></a>语法  
  
```sql
CERTPRIVATEKEY   
    (  
          cert_ID   
        , ' encryption_password '   
      [ , ' decryption_password ' ]  
    )  
```  
  
## <a name="arguments"></a>参数  
*certificate_ID*  
是**certificate_id**的证书。 这是可从 sys.certificates 或通过使用[CERT_ID &#40;Transact SQL &#41;](../../t-sql/functions/cert-id-transact-sql.md)函数。 *cert_id*是类型**int**
  
*encryption_password*  
用于对返回的二进制值进行加密的密码。
  
*decryption_password*  
用于对返回的二进制值进行解密的密码。
  
## <a name="return-types"></a>返回类型
**varbinary**
  
## <a name="remarks"></a>注释  
**CERTENCODED**和**CERTPRIVATEKEY**一起用于二进制形式返回证书的不同部分。
  
## <a name="permissions"></a>Permissions  
**CERTPRIVATEKEY**可供公用。
  
## <a name="examples"></a>示例  
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Use 5tr0ng P^55Words'  
GO  
CREATE CERTIFICATE Shipping04   
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20141031';  
GO  
SELECT CERTPRIVATEKEY(CERT_ID('Shipping04'), 'jklalkaa/; uia3dd');  
```  
  
有关的更复杂示例，使用**CERTPRIVATEKEY**和**CERTENCODED**若要将证书复制到另一个数据库，请参阅主题中的示例 B [CERTENCODED &#40;Transact SQL &#41;](../../t-sql/functions/certencoded-transact-sql.md).
  
## <a name="see-also"></a>另请参阅
[安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)  
[创建证书 &#40;Transact SQL &#41;](../../t-sql/statements/create-certificate-transact-sql.md) 
[安全函数 &#40;Transact SQL &#41;](../../t-sql/functions/security-functions-transact-sql.md) 
 [sys.certificates &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  

