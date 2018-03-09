---
title: sys.fn_my_permissions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_my_permissions_TSQL
- fn_my_permissions_TSQL
- sys.fn_my_permissions
- fn_my_permissions
dev_langs:
- TSQL
helpviewer_keywords:
- fn_my_permissions function
- sys.fn_my_permissions function
ms.assetid: 30f97f00-03d8-443a-9de9-9ec420b7699b
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3c83af3c3c59b52a4a7c9fb2e127ab3bd03fb87d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="sysfnmypermissions-transact-sql"></a>sys.fn_my_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有效授予主体对安全对象的权限的列表。 相关的函数是[HAS_PERMS_BY_NAME](../../t-sql/functions/has-perms-by-name-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
fn_my_permissions ( securable , 'securable_class' )  
```  
  
## <a name="arguments"></a>参数  
 *securable*  
 安全对象的名称。 如果安全对象为服务器或数据库，则该值应设置为 NULL。 *安全*是类型的标量表达式**sysname**。 *安全*可以是多部分名称。  
  
 '*securable_class*'  
 为其列出权限的安全对象的类的名称。 *securable_class*是**sysname**。 *securable_class*必须是以下之一： 应用程序角色、 程序集、 非对称密钥、 证书、 协定、 数据库、 终结点、 FULLTEXT CATALOG、 登录名、 消息类型、 对象、 REMOTE SERVICE BINDING、 角色、 路由、 架构、 服务器、 服务对称密钥、 类型、 用户、 XML 架构集合。  
  
## <a name="columns-returned"></a>返回的列  
 下表列出的列， **fn_my_permissions**返回。 返回的每一行说明了当前安全上下文拥有的对安全对象的一种权限。 如果查询失败，则返回 NULL。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|entity_name|**sysname**|对其有效授予所列权限的安全对象的名称。|  
|subentity_name|**sysname**|如果安全对象具有列，则为列名；否则为 NULL。|  
|permission_name|**nvarchar**|权限名称。|  
  
## <a name="remarks"></a>注释  
 该表值函数返回调用主体持有的对指定安全对象的有效权限的列表。 有效权限包括下列任何一种权限：  
  
-   直接授予主体并且不被拒绝的权限。  
  
-   由主体持有的更高级权限暗含的、且不被拒绝的权限。  
  
-   授予主体所属的角色或组的、且不被拒绝的权限。  
  
-   由主体所属的角色或组持有的、且不被拒绝的权限。  
  
 权限评估始终在调用方的安全上下文中执行。 若要确定其他某个主体是否具有有效的权限，调用方必须对该主体具有 IMPERSONATE 权限。  
  
 对于架构级实体，可接受由一部分、两部分或三部分组成的非空名称。 对于数据库级别的实体，一个部分名称接受，则具有 null 值的含义与"*当前数据库*"。 对于服务器本身，则需要一个 Null（表示“当前服务器”）。 **fn_my_permissions**无法检查对链接服务器的权限。  
  
 以下查询将返回内置安全对象类的列表：  
  
```  
SELECT DISTINCT class_desc FROM fn_builtin_permissions(default)  
    ORDER BY class_desc;  
GO  
```  
  
 如果默认提供的值作为*安全*或*securable_class*，则该值将被解释为 NULL。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-effective-permissions-on-the-server"></a>A. 列出对服务器的有效权限  
 以下示例返回调用方对服务器的有效权限的列表。  
  
```  
SELECT * FROM fn_my_permissions(NULL, 'SERVER');  
GO  
```  
  
### <a name="b-listing-effective-permissions-on-the-database"></a>B. 列出对数据库的有效权限  
 以下示例返回调用方对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的有效权限的列表。  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions (NULL, 'DATABASE');  
GO  
```  
  
### <a name="c-listing-effective-permissions-on-a-view"></a>C. 列出对视图的有效权限  
 以下示例返回调用方对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库内 `vIndividualCustomer` 架构中 `Sales` 视图的有效权限的列表。  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions('Sales.vIndividualCustomer', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;   
GO   
```  
  
### <a name="d-listing-effective-permissions-of-another-user"></a>D. 列出另一个用户的有效权限  
 以下示例返回数据库用户 `Wanida` 对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库内 `Employee` 架构中 `HumanResources` 表的有效权限的列表。 调用方需要对用户 `Wanida` 具有 IMPERSONATE 权限。  
  
```  
EXECUTE AS USER = 'Wanida';  
SELECT * FROM fn_my_permissions('HumanResources.Employee', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;    
REVERT;  
GO  
```  
  
### <a name="e-listing-effective-permissions-on-a-certificate"></a>E. 列出对证书的有效权限  
 以下示例返回调用方对当前数据库中证书 `Shipping47` 的有效权限的列表。  
  
```  
SELECT * FROM fn_my_permissions('Shipping47', 'CERTIFICATE');  
GO  
```  
  
### <a name="f-listing-effective-permissions-on-an-xml-schema-collection"></a>F. 列出对 XML 架构集合的有效权限  
 下面的示例返回上名为 XML 架构集合的调用方的有效权限列表`ProductDescriptionSchemaCollection`中[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库。  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions('ProductDescriptionSchemaCollection',  
    'XML SCHEMA COLLECTION');  
GO  
```  
  
### <a name="g-listing-effective-permissions-on-a-database-user"></a>G. 列出对数据库用户的有效权限  
 以下示例返回调用方对当前数据库中用户 `MalikAr` 的有效权限的列表。  
  
```  
SELECT * FROM fn_my_permissions('MalikAr', 'USER');  
GO  
```  
  
### <a name="h-listing-effective-permissions-of-another-login"></a>H. 列出另一个登录名的有效权限  
 以下示例返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `WanidaBenshoof` 对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库内 `Employee` 架构中 `HumanResources` 表的有效权限的列表。 调用方需要对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `WanidaBenshoof` 具有 IMPERSONATE 权限。  
  
```  
EXECUTE AS LOGIN = 'WanidaBenshoof';  
SELECT * FROM fn_my_permissions('AdventureWorks2012.HumanResources.Employee', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;    
REVERT;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)   
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [安全对象](../../relational-databases/security/securables.md)   
 [权限层次结构（数据库引擎）](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [执行 AS &#40;Transact SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  
