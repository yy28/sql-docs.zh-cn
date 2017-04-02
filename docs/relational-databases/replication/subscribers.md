---
title: "订阅服务器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subscribers.f1"
helpviewer_keywords: 
  - "订阅服务器 [SQL Server 复制]"
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# 订阅服务器
  指定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或非-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将接收对所选发布的订阅的订阅服务器。  
  
## 选项  
 **订阅服务器**  
 要启用相应的网格中选中的复选框 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或非-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上所选发布的订阅服务器数据源 **发布** 页。 如果没有列出订阅服务器，请单击 **“添加订阅服务器”** 或 **“添加 SQL Server 订阅服务器”**。  
  
 **订阅数据库**  
 在显示的信息和来自此列可执行的操作取决于订阅服务器中列出的类型 **订户** 列︰  
  
-   对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器，请从 **“订阅数据库”** 列表中选择订阅数据库，或从同一列表中选择 **“新建数据库”** 命令来创建新的数据库。  
  
    > [!NOTE]  
    >  若要启用发布服务器作为订阅服务器，则订阅数据库与发布数据库必须属于不同的数据库。  
  
-   对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器，不显示订阅数据库。 在指定的数据库，以及其他连接信息， **数据源名称** 字段 **添加非 SQL Server** 对话框。 此对话框可通过单击 **添加订阅服务器** ，然后单击 **添加非 SQL Server 订阅服务器**。  
  
 **添加订阅服务器**  
 向可以启用为订阅服务器的服务器列表中添加服务器。 如果以下条件全部为真，则显示此按钮：  
  
-   所选择的发布是不支持更新订阅的快照或事务发布。  
  
    > [!NOTE]  
    >  如果正在订阅的发布有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅，并且尚未为非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器启用发布，则不能添加非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅。  
  
-   订阅是推送订阅。  
  
-   所选发布的发布服务器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本。  
  
 单击 **添加订阅服务器** 显示一个菜单，其中包含两个选项︰ **添加 SQL Server 订阅服务器** 和 **添加非 SQL Server 订阅服务器**。 单击 **添加非 SQL Server 订阅服务器** 添加 Oracle 或 IBM DB2 订阅服务器。  
  
 **添加 SQL Server 订阅服务器**  
 向可以启用为订阅服务器的服务器列表中添加服务器。 如果以下一个或多个条件为真，则显示此按钮：  
  
-   所选择的发布是合并发布，或者是支持更新订阅的快照或事务发布。  
  
-   订阅是请求订阅。  
  
-   所选发布的发布服务器的版本早于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 对于早期版本，只有当以下一个或多个条件为真时才会显示该按钮：  
  
    -   您是发布服务器上 **sysadmin** 固定服务器角色的成员。  
  
    -   已在 **“发布服务器属性”** 对话框的 **“订阅服务器”** 页上添加了该订阅服务器。  
  
    -   发布允许匿名订阅。  
  
## 另请参阅  
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [创建推送订阅](../../relational-databases/replication/create-a-push-subscription.md)   
 [非 SQL Server 订阅服务器](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  