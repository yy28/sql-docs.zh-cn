---
title: "DISABLE TRIGGER (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DISABLE_TSQL
- DISABLE
- DISABLE TRIGGER
- DISABLE_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DML triggers, disabling
- DDL triggers, disabling
- DISABLE TRIGGER statement
- triggers [SQL Server], disabling
- disabling triggers
ms.assetid: e6529f06-e442-437e-a7bf-41790bc092c5
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 02888ae3de27c6859cd37bec9119761f4777b2bd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="disable-trigger-transact-sql"></a>DISABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  禁用触发器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DISABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *schema_name*  
 触发器所属架构的名称。 *schema_name*不能指定 DDL 或登录触发器。  
  
 *trigger_name*  
 要禁用的触发器的名称。  
  
 ALL  
 指示禁用在 ON 子句作用域中定义的所有触发器。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在为合并复制发布的数据库中创建触发器。 在已发布数据库中指定 ALL 可禁用这些触发器，这样会中断复制。 在指定 ALL 之前，请验证没有为合并复制发布当前数据库。  
  
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
 默认情况下，创建触发器后会启用触发器。 禁用触发器不会删除该触发器。 该触发器仍然作为对象存在于当前数据库中。 但是，当执行编写触发器程序所用的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句时，不会激发触发器。 可以通过使用重新启用触发器[ENABLE TRIGGER](../../t-sql/statements/enable-trigger-transact-sql.md)。 在表上定义的 DML 触发器可以为还应禁用或启用通过[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。  
  
 通过更改触发器**ALTER TRIGGER**语句启用触发器。  
  
## <a name="permissions"></a>Permissions  
 若要禁用 DML 触发器，用户必须至少对为其创建触发器的表或视图具有 ALTER 权限。  
  
 若要禁用具有服务器范围 (ON ALL SERVER) 的 DDL 触发器或登录触发器，用户必须对服务器拥有 CONTROL SERVER 权限。 若要禁用数据库范围 (ON DATABASE) 中的 DDL 触发器，用户必须至少对当前数据库具有 ALTER ANY DATABASE DDL TRIGGER 权限。  
  
## <a name="examples"></a>示例  
下面的示例将 AdventureWorks2012 数据库中所述。
  
### <a name="a-disabling-a-dml-trigger-on-a-table"></a>A. 禁用对表的 DML 触发器  
 以下示例禁用对表 `uAddress` 创建的触发器 `Address`。  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-disabling-a-ddl-trigger"></a>B. 禁用 DDL 触发器  
 以下示例在数据库范围创建 DDL 触发器 `safety`，然后禁用该触发器。  
  
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
```  
  
### <a name="c-disabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. 禁用以同一作用域定义的所有触发器  
 下例禁用在服务器范围内创建的所有 DDL 触发器。  
  
```  
DISABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ENABLE TRIGGER (Transact-SQL)](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [ALTER TRIGGER (Transact-SQL)](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER (Transact-SQL)](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers (Transact-SQL)](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  

