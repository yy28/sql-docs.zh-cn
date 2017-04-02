---
title: "启用或禁用数据收集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "数据收集器 [SQL Server], 禁用"
  - "数据收集器 [SQL Server], 启用"
ms.assetid: 0137971b-fb48-4a3e-822a-3df2b9bb09d7
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# 启用或禁用数据收集
  本主题介绍了如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中启用或禁用数据收集。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要启用或禁用数据收集，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 必须具有 **dc_admin** 或 **dc_operator**（拥有 EXECUTE 权限）固定数据库角色的成员身份才能执行此过程。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 启用数据收集器  
  
1.  在对象资源管理器中，展开 **“管理”** 节点。  
  
2.  右键单击“数据收集”，然后单击“启用数据收集”。  
  
#### 禁用数据收集器  
  
1.  在对象资源管理器中，展开 **“管理”** 节点。  
  
2.  右键单击“数据收集”，然后单击“禁用数据收集”。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 启用数据收集器  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 此示例使用 [sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md) 启用数据收集器。  
  
```tsql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_enable_collector ;  
```  
  
#### 禁用数据收集器  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 此示例使用 [sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md) 禁用数据收集器。  
  
```tsql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_disable_collector;  
```  
  
## 另请参阅  
 [数据收集](../../relational-databases/data-collection/data-collection.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  