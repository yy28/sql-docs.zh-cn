---
title: 管理触发器安全性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], security
ms.assetid: e94720a8-a3a2-4364-b0a3-bbe86e3ce4d5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9a290fd763adb52cc83213478103a93a47d3a274
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409516"
---
# <a name="manage-trigger-security"></a>管理触发器安全性
  默认情况下，在调用触发器的用户的上下文中执行 DML 和 DDL 触发器。 触发器的调用方是执行使触发器运行的语句的用户。 例如，如果用户 **Mary** 执行可以使 DML 触发器 **DML_trigMary** 运行的 DELETE 语句，则 **DML_trigMary** 中的代码将在 **Mary**的用户特权上下文中执行。 希望向数据库或服务器实例中引入恶意代码的用户可以使用此默认行为。 例如，用户 `JohnDoe`创建以下 DDL 触发器：  
  
 `CREATE TRIGGER DDL_trigJohnDoe`  
  
 `ON DATABASE`  
  
 `FOR ALTER_TABLE`  
  
 `AS`  
  
 `GRANT CONTROL SERVER TO JohnDoe ;`  
  
 `GO`  
  
 此触发器的含义是：在有权执行 `GRANT CONTROL SERVER` 语句的用户（如 **sysadmin** 固定服务器角色的成员）执行 `ALTER TABLE` 语句时，为 `JohnDoe` 授予 `CONTROL SERVER` 权限。 换言之，虽然 `JohnDoe` 不能为自己授予 `CONTROL SERVER` 权限，但是他启用了授予他此权限的触发器代码以在升级特权下执行。 对于此类安全隐患，DML 和 DDL 触发器都处于打开状态。  
  
## <a name="trigger-security-best-practices"></a>保证触发器安全的最佳方法  
 可以采取下列措施阻止触发器代码在升级特权下执行：  
  
-   注意数据库和服务器实例中存在的 DML 和 DDL 触发器，方法是查询 [sys.triggers](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql) 和 [sys.server_triggers](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql) 目录视图。 下面的查询将返回当前数据库中的所有 DML 触发器和数据库级别的 DDL 触发器，以及服务器实例中所有服务器级别的 DDL 触发器：  
  
    ```  
    SELECT type, name, parent_class_desc FROM sys.triggers  
    UNION  
    SELECT type, name, parent_class_desc FROM sys.server_triggers ;  
    ```  
  
-   使用 [DISABLE TRIGGER](/sql/t-sql/statements/disable-trigger-transact-sql) 禁用在升级特权下执行时可能会损害数据库或服务器完整性的触发器。 下面的语句可以禁用当前数据库中所有数据库级别的 DDL 触发器：  
  
    ```  
    DISABLE TRIGGER ALL ON DATABASE  
    ```  
  
     下面的语句可以禁用服务器实例中所有服务器级别的 DDL 触发器：  
  
    ```  
    DISABLE TRIGGER ALL ON ALL SERVER  
    ```  
  
     下面的语句可以禁用当前数据库中的所有 DML 触发器：  
  
    ```  
    DECLARE @schema_name sysname, @trigger_name sysname, @object_name sysname ;  
    DECLARE @sql nvarchar(max) ;  
    DECLARE trig_cur CURSOR FORWARD_ONLY READ_ONLY FOR  
        SELECT SCHEMA_NAME(schema_id) AS schema_name,  
            name AS trigger_name,  
            OBJECT_NAME(parent_object_id) as object_name  
        FROM sys.objects WHERE type in ('TR', 'TA') ;  
  
    OPEN trig_cur ;  
    FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        SELECT @sql = 'DISABLE TRIGGER ' + QUOTENAME(@schema_name) + '.'  
            + QUOTENAME(@trigger_name) +  
            ' ON ' + QUOTENAME(@schema_name) + '.'   
            + QUOTENAME(@object_name) + ' ; ' ;  
        EXEC (@sql) ;  
        FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
    END  
    GO  
  
    -- Verify triggers are disabled. Should return an empty result set.  
    SELECT * FROM sys.triggers WHERE is_disabled = 0 ;  
    GO  
  
    CLOSE trig_cur ;  
    DEALLOCATE trig_cur;  
    ```  
  
## <a name="see-also"></a>请参阅  
 [CREATE TRIGGER (Transact-SQL)](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DML 触发器](../triggers/dml-triggers.md)   
 [DDL 触发器](../triggers/ddl-triggers.md)  
  
  
