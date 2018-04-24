---
title: DENY 系统对象权限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, system objects
- encryption [SQL Server], system objects
- system objects [SQL Server]
- cryptography [SQL Server], system objects
ms.assetid: 4e43f954-0982-470b-a239-08a13c61563a
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1428cbd738588266c6090053dc8987724fbbf7a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="deny-system-object-permissions-transact-sql"></a>DENY 系统对象权限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  拒绝对系统对象（例如，存储过程、扩展存储过程、函数以及视图）的权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DENY { SELECT | EXECUTE } ON [ sys.]system_object TO principal   
```  
  
## <a name="arguments"></a>参数  
 [ **sys.**]  
 只有在引用目录视图和动态管理视图时才需要 sys 限定符。  
  
 system_object  
 指定要对其拒绝权限的对象。  
  
 principal  
 指定要从中撤消权限的主体。  
  
## <a name="remarks"></a>Remarks  
 可使用该语句拒绝对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装的特定存储过程、扩展存储过程、表值函数、标量函数、视图、目录视图、兼容性视图、INFORMATION_SCHEMA 视图、动态管理视图以及系统表的权限。 每个系统对象都作为唯一的一条记录存在于资源数据库 (mssqlsystemresource) 中。 该资源数据库为只读。 指向对象的链接作为各数据库的 sys 架构中的一条记录显示。  
  
 默认名称解析将解析资源数据库的非限定过程名称。 因此，只有在指定目录视图和动态管理视图时，才需要 **sys** 限定符。  
  
> [!CAUTION]  
>  拒绝对系统对象的权限会导致依赖这些权限的应用程序失败。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 使用目录视图，并且在更改了对目录视图的默认权限之后可能无法发挥预期的作用。  
  
 不支持拒绝对触发器以及对系统对象列的权限。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升级期间，对系统对象的权限将予以保留。  
  
 在 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) 目录视图中可以查看系统对象。 在 [master](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) 数据库中的 **sys.database_permissions** 目录视图中可以查看对系统对象的权限。  
  
 下面的查询将返回有关系统对象的权限的信息：  
  
```  
SELECT * FROM master.sys.database_permissions AS dp   
    JOIN sys.system_objects AS so  
    ON dp.major_id = so.object_id  
    WHERE dp.class = 1 AND so.parent_object_id = 0 ;  
GO  
```  
  
## <a name="permissions"></a>权限  
 需要 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例向 `EXECUTE` 拒绝了对 `xp_cmdshell` 的 `public` 权限。  
  
```  
DENY EXECUTE ON sys.xp_cmdshell TO public;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)   
 [sys.database_permissions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [GRANT 系统对象权限 (Transact-SQL)](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [REVOKE 系统对象权限 (Transact-SQL)](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)  
  
  
