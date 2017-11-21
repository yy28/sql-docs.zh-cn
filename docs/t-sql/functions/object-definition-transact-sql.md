---
title: "OBJECT_DEFINITION (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- OBJECT_DEFINITION_TSQL
- OBJECT_DEFINITION
dev_langs:
- TSQL
helpviewer_keywords:
- viewing source text
- source text [SQL Server]
- displaying source text
- OBJECT_DEFINITION function
ms.assetid: 2ac837c7-eca9-4d29-b06e-72e30450c68d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fcb2ac9e5dd80c804996d08b084b4b0068c4b618
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="objectdefinition-transact-sql"></a>OBJECT_DEFINITION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回指定对象的定义的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 源文本。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
OBJECT_DEFINITION ( object_id )  
```  
  
## <a name="arguments"></a>参数  
 *object_id*  
 要使用的对象的 ID。 *object_id*是**int**，和假定以表示当前的数据库上下文中的对象。  
  
## <a name="return-types"></a>返回类型  
 **nvarchar(max)**  
  
## <a name="exceptions"></a>异常  
 出现错误时或调用方没有查看对象的权限时，将返回 NULL。  
  
 用户只能查看符合如下条件的安全对象的元数据：该安全对象为该用户所有，或已授予该用户对该安全对象的权限。 这意味着，如果用户对对象没有任何权限，则元数据生成的内置函数（如 OBJECT_DEFINITION）可能返回 NULL。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]假定*object_id*位于当前数据库上下文中。 对象定义的排序规则始终与调用数据库上下文的排序规则匹配。  
  
 OBJECT_DEFINITION 适用于以下对象类型：  
  
-   C = 检查约束  
  
-   D = 默认值（约束或独立）  
  
-   P = SQL 存储过程  
  
-   FN = SQL 标量函数  
  
-   R = 规则  
  
-   RF = 复制筛选器过程  
  
-   TR = SQL 触发器（架构范围内的 DML 触发器，或数据库或服务器范围内的 DDL 触发器）  
  
-   IF = SQL 内联表值函数  
  
-   TF = SQL 表值函数  
  
-   V = 视图  
  
## <a name="permissions"></a>Permissions  
 系统对象定义对所有用户可见。 用户对象的定义对于对象所有者或具有下列任一权限的被授权者可见：ALTER、CONTROL、TAKE OWNERSHIP 或 VIEW DEFINITION。 **db_owner**、 **db_ddladmin**和 **db_securityadmin** 固定数据库角色的成员隐式具有这些权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-source-text-of-a-user-defined-object"></a>A. 返回用户定义对象的源文本  
 以下示例返回 `uAddress` 架构中的用户定义触发器 `Person` 的定义。 内置函数 `OBJECT_ID` 用于将触发器的对象 ID 返回到 `OBJECT_DEFINITION` 语句。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'Person.uAddress')) AS [Trigger Definition];   
GO  
```  
  
### <a name="b-returning-the-source-text-of-a-system-object"></a>B. 返回系统对象的源文本  
 以下示例返回系统存储过程 `sys.sp_columns` 的定义。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'sys.sp_columns')) AS [Object Definition];  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [元数据函数 &#40;Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_NAME &#40;Transact SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [OBJECT_ID &#40;Transact SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [sp_helptext (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.server_sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)  
  
  

