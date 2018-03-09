---
title: "ENABLE TRIGGER (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ENABLE TRIGGER
- ENABLE_TSQL
- ENABLE_TRIGGER_TSQL
- ENABLE
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, enabling
- triggers [SQL Server], enabling
- DML triggers, enabling
- ENABLE TRIGGER statement
ms.assetid: 6e21f0ad-68d0-432f-9c7c-a119dd2d3fc9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7627fdb66a091d5add30a8384861d9b6b03b82b5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="enable-trigger-transact-sql"></a>ENABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  启用 DML、DDL 或登录触发器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ENABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *schema_name*  
 触发器所属架构的名称。 *schema_name*不能指定 DDL 或登录触发器。  
  
 *trigger_name*  
 要启用的触发器的名称。  
  
 ALL  
 指示启用在 ON 子句作用域中定义的所有触发器。  
  
 *object_name*  
 是的名称的表或视图在其触发 DML *trigger_name*已创建以执行。  
  
 DATABASE  
 DDL 触发器，该值指示*trigger_name*已创建或修改与数据库作用域执行。  
  
 ALL SERVER  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 DDL 触发器，该值指示*trigger_name*已创建或修改要执行与服务器作用域。 ALL SERVER 也适用于登录触发器。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
## <a name="remarks"></a>注释  
 启用触发器并不是要重新创建它。 禁用的触发器仍以对象形式存在于当前数据库中，但并不激发。 启用触发器将导致在执行触发器最初编程时所针对的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句时激发。 使用禁用触发器[DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md)。 在表上定义的 DML 触发器可以为还应禁用或启用通过[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 若要启用 DML 触发器，用户必须至少对于创建触发器所在的表或视图拥有 ALTER 权限。  
  
 若要启用具有服务器作用域 (ON ALL SERVER) 的 DDL 触发器或登录触发器，用户必须对服务器具有 CONTROL SERVER 权限。 若要启用具有数据库范围 (ON DATABASE) 的 DDL 触发器，用户至少应在当前数据库中拥有 ALTER ANY DATABASE DDL TRIGGER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-enabling-a-dml-trigger-on-a-table"></a>A. 在表中启用 DML 触发器  
 下面的示例禁用触发器`uAddress`在表上创建`Address`在 AdventureWorks 数据库中，然后启用它。  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
ENABLE Trigger Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-enabling-a-ddl-trigger"></a>B. 启用 DDL 触发器  
 下面的示例创建 DDL 触发器`safety`与数据库作用域，然后禁用和启用它。  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
GO  
DISABLE TRIGGER safety ON DATABASE;  
GO  
ENABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-enabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. 启用以同一作用域定义的所有触发器  
 以下示例启用在服务器作用域级别创建的所有 DDL 触发器。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
ENABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [DISABLE TRIGGER (Transact-SQL)](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [ALTER TRIGGER (Transact-SQL)](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER (Transact-SQL)](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers (Transact-SQL)](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  
