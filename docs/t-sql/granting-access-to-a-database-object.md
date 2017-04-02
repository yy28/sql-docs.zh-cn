---
title: "授予访问数据库对象的权限 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "授予访问数据库对象的权限"
ms.assetid: a44d9bbf-f58e-4734-b7f4-eb3b492b777b
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 授予访问数据库对象的权限
作为管理员，可以从 **Products** 表和 **vw_Names** 视图执行 Select，以及执行 **pr_Names** 过程；但是 Mary 不能。 若要授予 Mary 必要的权限，请使用 GRANT 语句。  
  
### 过程标题  
  
1.  执行以下语句将 `Mary` 存储过程的 `EXECUTE` 权限授予 `pr_Names`。  
  
    ```  
    GRANT EXECUTE ON pr_Names TO Mary;  
    GO  
    ```  
  
在这种情况下，Mary 只能通过使用存储过程访问 **Products** 表。 如果您希望 Mary 能够对视图执行 SELECT 语句，则您还必须执行 `GRANT SELECT ON vw_Names TO Mary`。 若要删除对数据库对象的访问权限，请使用 REVOKE 语句。  
  
> [!NOTE]  
> 如果表、视图和存储过程不是由同一架构拥有，则授予权限将变得更复杂。  
  
## 关于 GRANT  
必须具有 EXECUTE 权限才能执行存储过程。 必须具有 SELECT、INSERT、UPDATE 和 DELETE 权限才能访问和更改数据。 GRANT 语句还用于其他权限，如创建表的权限。  
  
## 课程中的下一个任务  
[摘要：配置数据库对象的权限](../t-sql/summary-configuring-permissions-on-database-objects.md)  
  
## 另请参阅  
[GRANT (Transact-SQL)](../t-sql/statements/grant-transact-sql.md)  
[REVOKE (Transact-SQL)](../t-sql/statements/revoke-transact-sql.md)  
  
  
  
