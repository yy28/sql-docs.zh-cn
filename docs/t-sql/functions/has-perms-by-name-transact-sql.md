---
title: "HAS_PERMS_BY_NAME (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HAS_PERMS_BY_NAME
- HAS_PERMS_BY_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- current permission status
- checking permission status
- verifying permission status
- testing permissions
- HAS_PERMS_BY_NAME function
ms.assetid: eaf8cc82-1047-4144-9e77-0e1095df6143
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 09eae4a5ea247592109c0fcbc261f1ec3ce1b3db
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="haspermsbyname-transact-sql"></a>HAS_PERMS_BY_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  评估当前用户对安全对象的有效权限。 相关的函数是[fn_my_permissions](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
HAS_PERMS_BY_NAME ( securable , securable_class , permission    
    [ , sub-securable ] [ , sub-securable_class ] )  
```  
  
## <a name="arguments"></a>参数  
 *安全对象*  
 安全对象的名称。 如果安全对象是服务器本身，则此值应设置为 NULL。 *安全*是类型的标量表达式**sysname**。 没有默认值。  
  
 *securable_class*  
 测试权限的安全对象的类名。 *securable_class*是类型的标量表达式**nvarchar(60)**。  
  
 在[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，securable_class 参数必须设置为以下项之一：**数据库**，**对象**，**角色**，**架构**，或**用户**。  
  
 *权限*  
 类型的非空标量表达式**sysname** ，表示要检查的权限名称。 没有默认值。 权限名称 ANY 是通配符。  
  
 *子安全对象*  
 类型的可选标量表达式**sysname** ，它表示对其测试权限的安全对象子实体的名称。 默认值为 NULL。  
  
> [!NOTE]  
>  在新版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，子安全对象不能在窗体中使用括号**[***子名称***]**。 使用*子名称*相反。  
  
 *sub securable_class*  
 类型的可选标量表达式**nvarchar(60)** ，可表示的对其测试权限的安全对象 subentity 类。 默认值为 NULL。  
  
 在[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，子 securable_class 自变量无效，只有当 securable_class 参数设置为**对象**。 如果 securable_class 参数设置为**对象**，子 securable_class 参数必须设置为**列**。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
 如果查询失败，则返回 NULL。  
  
## <a name="remarks"></a>注释  
 此内置函数将测试当前主体对于指定的安全对象是否具有特定的有效权限。 如果用户具有针对安全对象的有效权限，HAS_PERMS_BY_NAME 返回 1；如果用户不具有针对安全对象的有效权限，返回 0；如果安全对象类或权限无效，返回 NULL。 有效权限可以是下列任意一种：  
  
-   直接授予主体并且不被拒绝的权限。  
  
-   由主体持有的更高级权限暗含的、且不被拒绝的权限。  
  
-   授予主体所属的角色或组的、且不被拒绝的权限。  
  
-   由主体所属的角色或组持有的、且不被拒绝的权限。  
  
 权限评估始终在调用方的安全上下文中执行。 若要确定某些其他用户是否具有有效权限，调用方必须对此用户具有 IMPERSONATE 权限。  
  
 对于架构级实体，可接受由一部分、两部分或三部分组成的非空名称。 对于数据库级实体，只接受由一部分组成的名称，Null 表示“当前数据库”。 对于服务器本身，则需要一个 Null（表示“当前服务器”）。 此函数无法针对尚未创建服务器级主体的已链接服务器或 Windows 用户进行权限检查。  
  
 以下查询将返回内置安全对象类的列表：  
  
```  
SELECT class_desc FROM sys.fn_builtin_permissions(default);  
```  
  
 使用以下排序规则：  
  
-   当前数据库排序规则：包括架构未包含的安全对象的数据库级安全对象；由一部分或两部分组成的架构范围内的安全对象；使用由三部分组成的名称时的目标数据库。  
  
-   master 数据库排序规则：服务器级安全对象。  
  
-   列级别检查不支持“ANY”。 必须指定合适的权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-do-i-have-the-server-level-view-server-state-permission"></a>A. 我具有服务器级 VIEW SERVER STATE 权限吗？  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT HAS_PERMS_BY_NAME(null, null, 'VIEW SERVER STATE');  
```  
  
### <a name="b-am-i-able-to-impersonate-server-principal-ps"></a>B. 我可以 IMPERSONATE 服务器主体 Ps 吗？  
  
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT HAS_PERMS_BY_NAME('Ps', 'LOGIN', 'IMPERSONATE');  
```  
  
### <a name="c-do-i-have-any-permissions-in-the-current-database"></a>C. 我在当前数据库中具有任何权限吗？  
  
```  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'ANY');  
```  
  
### <a name="d-does-database-principal-pd-have-any-permission-in-the-current-database"></a>D. 数据库主体 Pd 在当前数据库中具有任何权限吗？  
 假定调用方对主体 `Pd` 有 IMPERSONATE 权限。  
  
```  
EXECUTE AS user = 'Pd'  
GO  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'ANY');  
GO  
REVERT;  
GO  
```  
  
### <a name="e-can-i-create-procedures-and-tables-in-schema-s"></a>E. 我可以在架构 S 中创建过程和表吗？  
 以下示例需要在 `ALTER` 中具有 `S` 权限，在数据库中具有 `CREATE PROCEDURE` 权限，表的情况与此类似。  
  
```  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'CREATE PROCEDURE')  
    & HAS_PERMS_BY_NAME('S', 'SCHEMA', 'ALTER') AS _can_create_procs,  
    HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'CREATE TABLE') &  
    HAS_PERMS_BY_NAME('S', 'SCHEMA', 'ALTER') AS _can_create_tables;  
```  
  
### <a name="f-which-tables-do-i-have-select-permission-on"></a>F. 我对哪些表具有 SELECT 权限？  
  
```  
SELECT HAS_PERMS_BY_NAME  
(QUOTENAME(SCHEMA_NAME(schema_id)) + '.' + QUOTENAME(name),   
    'OBJECT', 'SELECT') AS have_select, * FROM sys.tables  
```  
  
### <a name="g-do-i-have-insert-permission-on-the-salesperson-table-in-adventureworks2012"></a>G. 我对 AdventureWorks2012 中的 SalesPerson 表有 INSERT 权限吗？  
 以下示例假定 `AdventureWorks2012` 为我的当前数据库上下文，并使用由两部分组成的名称。  
  
```  
SELECT HAS_PERMS_BY_NAME('Sales.SalesPerson', 'OBJECT', 'INSERT');  
```  
  
 以下示例对我的当前数据库上下文未做任何假定，并使用由三部分组成的名称。  
  
```  
SELECT HAS_PERMS_BY_NAME('AdventureWorks2012.Sales.SalesPerson',   
    'OBJECT', 'INSERT');  
```  
  
### <a name="h-which-columns-of-table-t-do-i-have-select-permission-on"></a>H. 我对 T 表的哪些列有 SELECT 权限？  
  
```  
SELECT name AS column_name,   
    HAS_PERMS_BY_NAME('T', 'OBJECT', 'SELECT', name, 'COLUMN')   
    AS can_select   
    FROM sys.columns AS c   
    WHERE c.object_id=object_id('T');  
```  
  
## <a name="see-also"></a>另请参阅  
 [权限（数据库引擎）](../../relational-databases/security/permissions-database-engine.md)   
 [安全对象](../../relational-databases/security/securables.md)   
 [权限层次结构（数据库引擎）](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
  
  

