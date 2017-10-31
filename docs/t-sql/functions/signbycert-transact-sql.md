---
title: "SIGNBYCERT (Transact SQL) |Microsoft 文档"
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
- SIGNBYCERT
- SIGNBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- text signing [SQL Server]
- encryption [SQL Server], certificates
- certificates [SQL Server], text signing
- SignByCert function
- signing text [SQL Server]
- SIGNBYCERT function
- cryptography [SQL Server], certificates
ms.assetid: b4c6bced-4473-4bae-85b9-56deced495f9
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b753e29b576d70b8c77dc40b570ab10dc314f22e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="signbycert-transact-sql"></a>SIGNBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使用证书对文本进行签名并返回签名。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SignByCert ( certificate_ID , @cleartext [ , 'password' ] )  
```  
  
## <a name="arguments"></a>参数  
 *certificate_ID*  
 当前数据库中证书的 ID。 *certificate_ID*是**int**。  
  
 *@cleartext*  
 是类型的变量**nvarchar**， **char**， **varchar**，或**nchar**包含将签名的数据。  
  
  *密码*   
 用来对证书私钥进行加密的密码。 *密码*是**nvarchar （128)**。  
  
## <a name="return-types"></a>返回类型  
 **varbinary** 8000 个字节的最大大小。  
  
## <a name="remarks"></a>注释  
 需要对证书具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 下面的示例在登录文本`@SensitiveData`使用证书`ABerglundCert07`，具有第一次解密密码"pGFD4bb925DGvbd2439587y"的证书。 然后，它在 `SignedData04` 表中插入明文和签名。  
  
```  
DECLARE @SensitiveData nvarchar(max);  
SET @SensitiveData = N'Saddle Price Points are   
    2, 3, 5, 7, 11, 13, 17, 19, 23, 29';  
INSERT INTO [SignedData04]  
    VALUES( N'data signed by certificate ''ABerglundCert07''',  
    @SensitiveData, SignByCert( Cert_Id( 'ABerglundCert07' ),   
    @SensitiveData, N'pGFD4bb925DGvbd2439587y' ));  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [VERIFYSIGNEDBYCERT &#40;Transact SQL &#41;](../../t-sql/functions/verifysignedbycert-transact-sql.md)   
 [CERT_ID &#40;Transact SQL &#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [删除证书 &#40;Transact SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

