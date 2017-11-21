---
title: "IS_OBJECTSIGNED (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/10/2016
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
- IS_OBJECTSIGNED
- IS_OBJECTSIGNED_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IS_OBJECTSIGNED function
ms.assetid: afbc4f7f-8266-4ee6-9802-14a2dbe69ef6
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e346fb803e18d9a43afe15984166985ff0a3e408
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

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
 **OBJECT**  
 安全对象类的类型。  
  
 *@object_id*  
 要测试的对象的 object_id。 *@object_id*是类型**int**。  
  
 *@class*  
 对象的类：  
  
-   “证书”  
  
-   “非对称密钥”  
  
 *@class*是**sysname**。  
  
 *@thumbprint*  
 对象的 SHA 指纹。 *@thumbprint*是类型**varbinary(32)**。  
  
## <a name="returned-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>注释  
 IS_OBJECTSIGNED 返回以下值。  
  
|返回值|Description|  
|------------------|-----------------|  
|NULL|对象未签名，或对象无效。|  
|0|对象已签名，但签名无效。|  
|1|该对象已签名。|  
  
## <a name="permissions"></a>Permissions  
 要求对证书或非对称密钥拥有 VIEW DEFINITION 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-displaying-extended-properties-on-a-database"></a>A. 显示数据库的扩展属性  
 下面的示例测试如果 spt_fallback_db 表中**master**数据库进行签名的签名证书的架构。  
  
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
 [sys.fn_check_object_signatures &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-check-object-signatures-transact-sql.md)  
  
  

