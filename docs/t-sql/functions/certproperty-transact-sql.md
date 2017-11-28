---
title: "CERTPROPERTY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
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
- CERTPROPERTY
- CERTPROPERTY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- certificates [SQL Server], schema names
- schemas [SQL Server], names
- CERTPROPERTY function
ms.assetid: 966c09aa-bc4e-45b0-ba53-c8381871f638
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d63968d8b07a37ea49662bd0727632a1675b3913
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="certproperty-transact-sql"></a>CERTPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回指定证书属性的值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
CertProperty ( Cert_ID , '<PropertyName>' )  
  
<PropertyName> ::=  
   Expiry_Date | Start_Date | Issuer_Name   
   | Cert_Serial_Number | Subject | SID | String_SID   
```  
  
## <a name="arguments"></a>参数  
*Cert_ID*  
证书的 ID。 *Cert_ID*是整数。
  
*Expiry_Date*  
证书的失效日期。
  
*Start_Date*  
证书开始生效的日期。
  
*Issuer_Name*  
证书颁发者的名称。
  
*Cert_Serial_Number*  
证书序列号。
  
*主题*  
证书的主题。
  
 *SID*  
证书的 SID。 这也是映射到该证书的所有登录或用户的 SID。
  
*String_SID*  
字符串形式的证书的 SID。 这也是映射到该证书的所有登录或用户的 SID。
  
## <a name="return-types"></a>返回类型
属性规范必须以单引号 (') 括起。
  
返回类型取决于在函数调用中指定的属性。 所有返回值将封装的返回类型在**sql_variant**。
-   *Expiry_Date*和*Start_Date*返回**datetime**。  
-   *Cert_Serial_Number*， *Issuer_Name*，*主题*，和*String_SID*返回**nvarchar**。  
-   *SID*返回**varbinary**。  
  
## <a name="remarks"></a>注释  
有关证书的信息会显示在[sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)目录视图。
  
## <a name="permissions"></a>Permissions  
需要对证书具有某些权限，并且未拒绝向调用方授予该证书的 VIEW DEFINITION 权限。
  
## <a name="examples"></a>示例  
以下示例返回证书主题。
  
```sql
-- First create a certificate.  
CREATE CERTIFICATE Marketing19 WITH   
    START_DATE = '04/04/2004' ,  
    EXPIRY_DATE = '07/07/2007' ,  
    SUBJECT = 'Marketing Print Division';  
GO  
  
-- Now use CertProperty to examine certificate  
-- Marketing19's properties.  
DECLARE @CertSubject sql_variant;  
set @CertSubject = CertProperty( Cert_ID('Marketing19'), 'Subject');  
PRINT CONVERT(nvarchar, @CertSubject);  
GO  
```  
  
## <a name="see-also"></a>另请参阅
[CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)  
[ALTER CERTIFICATE &#40;Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)  
[CERT_ID &#40;Transact SQL &#41;](../../t-sql/functions/cert-id-transact-sql.md) 
[加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)
[sys.certificates &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 
[安全性目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  
