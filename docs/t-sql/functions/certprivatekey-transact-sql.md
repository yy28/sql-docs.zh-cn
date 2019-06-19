---
title: CERTPRIVATEKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CERTPRIVATEKEY
- CERTPRIVATEKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTPRIVATEKEY
ms.assetid: 33e0f01e-39ac-46da-94ff-fe53b1116df4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e409d5064cb0e807d12a76b42055a6a43c9cb7c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948824"
---
# <a name="certprivatekey-transact-sql"></a>CERTPRIVATEKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

此函数返回二进制格式的证书私钥。 此函数有三个参数。
-   一个证书 ID。  
-   一个加密密码，用于加密函数返回的私钥位。 这种方法不会以明文文本形式向用户显示密钥。  
-   一个可选的解密密码。 指定的解密密码用于解开此证书的私钥。 否则，使用数据库主密钥。  
  
只有可以访问证书私钥的用户可以使用此函数。 此函数返回 PVK 格式的私钥。
  
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
certificate_ID   
证书的 certificate_id  。 通过 sys.certificates 或通过 [CERT_ID (Transact-SQL)](../../t-sql/functions/cert-id-transact-sql.md) 函数获得此值。 cert_id 为 int 数据类型   。
  
encryption_password   
用于对返回的二进制值进行加密的密码。
  
decryption_password   
用于对返回的二进制值进行解密的密码。
  
## <a name="return-types"></a>返回类型
**varbinary**
  
## <a name="remarks"></a>Remarks  
同时使用 CERTENCODED 和 CERTPRIVATEKEY 以二进制格式返回证书的其他部分   。
  
## <a name="permissions"></a>权限  
CERTPRIVATEKEY 向用户开放使用  。
  
## <a name="examples"></a>示例  
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Use 5tr0ng P^55Words'  
GO  
CREATE CERTIFICATE Shipping04   
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20401031';  
GO  
SELECT CERTPRIVATEKEY(CERT_ID('Shipping04'), 'jklalkaa/; uia3dd');  
```  
  
请参阅 [CERTENCODED (Transact-SQL)](../../t-sql/functions/certencoded-transact-sql.md) 中的示例 B，查看有关使用 CERTPRIVATEKEY 和 CERTENCODED 将证书复制到其他数据库中的更为复杂的示例   。
  
## <a name="see-also"></a>另请参阅
[安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)  
[CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)
[安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)
[sys.certificates (Transact-SQL)](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
