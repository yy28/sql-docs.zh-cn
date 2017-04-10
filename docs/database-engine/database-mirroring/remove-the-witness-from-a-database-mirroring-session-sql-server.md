---
title: "从数据库镜像会话删除见证服务器 (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "见证服务器 [SQL Server], 关闭"
  - "见证服务器 [SQL Server], 删除"
  - "数据库镜像 [SQL Server], 见证服务器"
ms.assetid: f3ce7afc-8936-4d35-80ce-d0f8fbc318d3
caps.latest.revision: 39
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 39
---
# 从数据库镜像会话删除见证服务器 (SQL Server)
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中从数据库镜像会话中删除见证服务器。 在数据库镜像会话期间的任何时候，数据库所有者都可以关闭数据库镜像会话的见证服务器。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **删除见证服务器，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **跟进：**[删除见证服务器之后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 需要对数据库拥有 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 删除见证服务器  
  
1.  连接至主体服务器实例，在 **对象资源管理器** 窗格中，单击服务器名称以展开服务器树。  
  
2.  展开 **“数据库”**，并选择要删除其见证服务器的数据库。  
  
3.  右键单击数据库，选择“任务”，再单击“镜像”。 这样便可打开 **“数据库属性”** 对话框的 **“镜像”** 页。  
  
4.  若要删除见证服务器，请从 **“见证服务器”** 字段中删除它的服务器网络地址。  
  
    > [!NOTE]  
    >  如果从具有自动故障转移功能的高安全性模式切换到高性能模式，则将自动清除“见证服务器”字段。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 删除见证服务器  
  
1.  连接到任一伙伴服务器实例上的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  发出以下语句：  
  
     [ALTER DATABASE](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md) *database_name* SET WITNESS OFF  
  
     其中，*database_name* 为镜像数据库的名称。  
  
     以下示例从 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中删除见证服务器。  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET WITNESS OFF ;  
    ```  
  
##  <a name="FollowUp"></a> 跟进：删除见证服务器之后  
 关闭见证服务器将根据事务安全设置更改[运行模式](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)：  
  
-   如果事务安全设置为 FULL（默认值），则会话将使用不带自动故障转移的高安全同步模式。  
  
-   如果事务安全设置为 OFF，则会话将异步运行（在高性能模式下），而无需仲裁。 强烈建议您只要事务安全关闭，就也应当关闭见证服务器。  
  
> [!TIP]  
>  数据库的事务安全性设置记录在每个伙伴的 [sys.database_mirroring](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md) 目录视图中的 **mirroring_safety_level** 和 **mirroring_safety_level_desc** 列内。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [使用 Windows 身份验证添加数据库镜像见证服务器 (Transact-SQL)](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
-   [添加或替换数据库镜像见证服务器 (SQL Server Management Studio)](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
## 另请参阅  
 [ALTER DATABASE 数据库镜像 (Transact-SQL)](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md)   
 [更改数据库镜像会话中的事务安全 (Transact-SQL)](../../database-engine/database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)   
 [使用 Windows 身份验证添加数据库镜像见证服务器 (Transact-SQL)](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)   
 [数据库镜像见证服务器](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  