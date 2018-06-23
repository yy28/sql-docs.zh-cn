---
title: 删除或禁用 DML 触发器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-dml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- DML triggers, disabling
- removing DML triggers
- disabling DML triggers
- dropping DML triggers
- deleting DML triggers
- DML triggers, removing
ms.assetid: 0f97f953-33c5-4b26-afeb-db2a26ce38b4
caps.latest.revision: 26
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6cdf4448c8286e8b461d9e83a45fd96c15fe94ba
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017277"
---
# <a name="delete-or-disable-dml-triggers"></a>删除或禁用 DML 触发器
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中删除或禁用 DML 触发器。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
     [Security](#Security)  
  
-   **若要删除或禁用 DML 触发器，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
  
-   删除了触发器后，它就从当前数据库中删除了。 它所基于的表和数据不会受到影响。 删除表将自动删除其上的所有触发器。  
  
-   在创建触发器时，触发器默认为启用状态。  
  
-   禁用触发器不会删除该触发器。 该触发器仍然作为对象存在于当前数据库中。 但是，当执行任意 INSERT、UPDATE 或 DELETE 语句（在其上对触发器进行了编程）时，触发器将不会激发。 已禁用的触发器可以被重新启用。 启用触发器并不是要重新创建它。 触发器将以最初创建它时的方式激发。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 若要删除 DML 触发器，要求对要定义触发器的表或视图具有 ALTER 权限。  
  
 若要禁用或启用 DML 触发器，用户必须至少对为其创建触发器的表或视图具有 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-dml-trigger"></a>删除 DML 触发器  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，然后展开该实例。  
  
2.  展开您所需的数据库，再展开 **“表”**，然后展开包含要删除的触发器的表。  
  
3.  展开 **“触发器”**，右键单击要删除的触发器，再单击 **“删除”**。  
  
4.  在 **“删除对象”** 对话框中，确认要删除的触发器，然后单击 **“确定”**。  
  
#### <a name="to-disable-and-enable-a-dml-trigger"></a>禁用和启用 DML 触发器  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，然后展开该实例。  
  
2.  展开您所需的数据库，再展开 **“表”**，然后展开包含要禁用的触发器的表。  
  
3.  展开 **“触发器”**，右键单击要禁用的触发器，再单击 **“禁用”**。  
  
4.  若要启用触发器，请单击 **“启用”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-dml-trigger"></a>删除 DML 触发器  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  复制以下示例并将其粘贴到查询窗口中。 执行 [CREATE TRIGGER](/sql/t-sql/statements/create-trigger-transact-sql) 语句以创建 `Sales.bonus_reminder` 触发器。 若要删除该触发器，请执行 [DROP TRIGGER](/sql/t-sql/statements/drop-trigger-transact-sql) 语句。  
  
```tsql  
--Create the trigger.  
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
--Delete the trigger.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('Sales.bonus_reminder', 'TR') IS NOT NULL  
   DROP TRIGGER Sales.bonus_reminder;  
GO  
  
```  
  
#### <a name="to-disable-and-enable-a-dml-trigger"></a>禁用和启用 DML 触发器  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  复制以下示例并将其粘贴到查询窗口中。 执行 [CREATE TRIGGER](/sql/t-sql/statements/create-trigger-transact-sql) 语句以创建 `Sales.bonus_reminder` 触发器。 若要禁用和启用该触发器，请分别执行 [DISABLE TRIGGER](/sql/t-sql/statements/disable-trigger-transact-sql) 语句和 [ENABLE TRIGGER](/sql/t-sql/statements/enable-trigger-transact-sql) 语句。  
  
```tsql  
--Create the trigger.  
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
--Disable the trigger.  
USE AdventureWorks2012;  
GO  
DISABLE TRIGGER Sales.bonus_reminder ON Sales.SalesPersonQuotaHistory;  
GO  
  
```  
  
```tsql  
--Enable the trigger.  
USE AdventureWorks2012;  
GO  
ENABLE TRIGGER Sales.bonus_reminder ON Sales.SalesPersonQuotaHistory;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [ALTER TRIGGER (Transact-SQL)](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [CREATE TRIGGER (Transact-SQL)](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DROP TRIGGER (Transact-SQL)](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [ENABLE TRIGGER (Transact-SQL)](/sql/t-sql/statements/enable-trigger-transact-sql)   
 [DISABLE TRIGGER (Transact-SQL)](/sql/t-sql/statements/disable-trigger-transact-sql)   
 [EVENTDATA (Transact-SQL)](/sql/t-sql/functions/eventdata-transact-sql)   
 [获取有关 DML 触发器的信息](dml-triggers.md)   
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
  
  
