---
title: IS_OBJECTSIGNED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IS_OBJECTSIGNED
- IS_OBJECTSIGNED_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IS_OBJECTSIGNED function
ms.assetid: afbc4f7f-8266-4ee6-9802-14a2dbe69ef6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1891180d7fa3b1a064cf0cdebc5295303ecf7b5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086701"
---
# <a name="isobjectsigned-transact-sql"></a>IS_OBJECTSIGNED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指示对象由指定证书或非对称密钥签名。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
IS_OBJECTSIGNED (   
'OBJECT', @object_id, @class, @thumbprint  
  )   
```  
  
## <a name="arguments"></a>参数  
 **'OBJECT'**  
 安全对象类的类型。  
  
 *@object_id*  
 要测试的对象的 object_id。 @object_id 的类型为 int   。  
  
 *@class*  
 对象的类：  
  
-   “证书”  
  
-   “非对称密钥”  
  
 @class 的数据类型为 sysname   。  
  
 *@thumbprint*  
 对象的 SHA 指纹。 @thumbprint 的类型为 varbinary(32)   。  
  
## <a name="returned-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 IS_OBJECTSIGNED 返回以下值。  
  
|返回值|描述|  
|------------------|-----------------|  
|NULL|对象未签名，或对象无效。|  
|0|对象已签名，但签名无效。|  
|1|该对象已签名。|  
  
## <a name="permissions"></a>权限  
 要求对证书或非对称密钥拥有 VIEW DEFINITION 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-displaying-extended-properties-on-a-database"></a>A. 显示数据库的扩展属性  
 下面的示例测试 master 数据库中的 spt_fallback_db 表是否由架构签名证书进行签名  。  
  
```  
USE master;  
-- Declare a variable to hold a thumbprint and an object name  
DECLARE @thumbprint varbinary(20), @objectname sysname;  
  
-- Populate the thumbprint variable with the thumbprint of   
-- the master database schema signing certificate  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%';  
  
-- Populate the object name variable with a table name in master  
SELECT @objectname = 'spt_fallback_db';  
  
-- Query to see if the table is signed by the thumbprint  
SELECT @objectname AS [object name],  
IS_OBJECTSIGNED(  
'OBJECT', OBJECT_ID(@objectname), 'certificate', @thumbprint  
) AS [Is the object signed?] ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.fn_check_object_signatures (Transact-SQL)](../../relational-databases/system-functions/sys-fn-check-object-signatures-transact-sql.md)  
  
  
