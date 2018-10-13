---
title: 修改或重命名 DML 触发器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- renaming triggers
- modifying triggers
- DML triggers, modifying
ms.assetid: c7317eec-c0e9-479e-a4a7-83b6b6c58d59
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3eced987f2f19e5379ab14ebc88eca37b8e19d8a
ms.sourcegitcommit: 0d6e4cafbb5d746e7d00fdacf8f3ce16f3023306
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2018
ms.locfileid: "49084966"
---
# <a name="modify-or-rename-dml-triggers"></a>修改或重命名 DML 触发器
  本主题将说明如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]修改或重命名 DML 触发器。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
     [Security](#Security)  
  
-   **若要修改或重命名 DML 触发器，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   重命名触发器时，该触发器必须位于当前数据库中，并且新名称必须遵守 [标识符](../databases/database-identifiers.md)规则。  
  
###  <a name="Recommendations"></a> 建议  
  
-   我们建议你不要使用 [sp_rename](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql) 存储过程重命名触发器。 更改对象名的任一部分都可能破坏脚本和存储过程。 重命名触发器将不会更改 [sys.sql_modules](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql) 目录视图的定义列中相应对象名的名称。 我们建议你删除并重新创建触发器。  
  
-   如果更改了 DML 触发器引用的对象名，则必须修改触发器以使其文本反映新的名称。 因此，在重命名对象之前，需要先显示该对象的依赖关系，以确定所建议的更改是否会影响任何触发器。  
  
-   也可以修改 DML 触发器以加密其定义。  
  
-   若要查看触发器的依赖项，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或以下函数和目录视图：  
  
    -   [sys.sql_expression_dependencies (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
    -   [sys.dm_sql_referenced_entities (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
    -   [sys.dm_sql_referencing_entities (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql)  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 若要更改 DML 触发器，需要对于定义该触发器所在的表或视图拥有 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-dml-trigger"></a>修改 DML 触发器  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 的实例，然后展开该实例。  
  
2.  展开您所需的数据库，再展开 **“表”**，然后展开包含要修改的触发器的表。  
  
3.  展开 **“触发器”**，右键单击要修改的触发器，然后单击 **“修改”**。  
  
4.  修改该触发器，然后单击 **“执行”**。  
  
#### <a name="to-rename-a-dml-trigger"></a>重命名 DML 触发器  
  
1.  [删除要重命名的触发器](../triggers/dml-triggers.md) 。  
  
2.  [重新创建触发器](../triggers/create-dml-triggers.md)，指定新名称。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-modify-a-trigger-using-alter-trigger"></a>使用 ALTER TRIGGER 修改触发器  
  
1.  连接到[!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  复制并将以下示例粘贴到查询中。 执行第一个示例以创建 DML 触发器，在用户尝试添加或更改 `SalesPersonQuotaHistory` 表中的数据时，该触发器将用户定义的信息打印到客户端。 执行 [ALTER TRIGGER](/sql/t-sql/statements/alter-trigger-transact-sql) 语句修改该触发器以便仅对 `INSERT` 活动激发。 此触发器十分有用，因为它可提醒向此表中插入行或更新行的用户也要通知 `Compensation` 部门。  
  
```tsql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;  
GO  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
#### <a name="to-rename-a-trigger-using-drop-trigger-and-alter-trigger"></a>若要重命名触发器，请使用 DROP TRIGGER 和 ALTER TRIGGER  
  
1.  连接到[!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 该示例使用 [DROP TRIGGER](/sql/t-sql/statements/drop-trigger-transact-sql) 和 [ALTER TRIGGER](/sql/t-sql/statements/alter-trigger-transact-sql) 语句将 `Sales.bonus_reminder` 触发器重命名为 `Sales.bonus_reminder_2`。  
  
```tsql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder_2  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
## <a name="see-also"></a>请参阅  
 [CREATE TRIGGER (Transact-SQL)](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DROP TRIGGER (Transact-SQL)](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [ENABLE TRIGGER (Transact-SQL)](/sql/t-sql/statements/enable-trigger-transact-sql)   
 [DISABLE TRIGGER (Transact-SQL)](/sql/t-sql/statements/disable-trigger-transact-sql)   
 [EVENTDATA (Transact-SQL)](/sql/t-sql/functions/eventdata-transact-sql)   
 [sp_rename (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql)   
 [ALTER TRIGGER (Transact-SQL)](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [获取有关 DML 触发器的信息](../triggers/get-information-about-dml-triggers.md)   
 [sp_help (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-help-transact-sql)   
 [sp_helptrigger (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helptrigger-transact-sql)   
 [sys.triggers (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql)   
 [sys.trigger_events (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-trigger-events-transact-sql)   
 [sys.sql_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)   
 [sys.assembly_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)   
 [sys.server_triggers (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)   
 [sys.server_trigger_events (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)   
 [sys.server_sql_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql)   
 [sys.server_assembly_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)  
  
  
