---
title: "允许非管理员使用复制监视器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "复制监视器, 非管理员访问"
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 允许非管理员使用复制监视器
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中允许非管理员使用复制监视器。 属于下列角色成员的用户可以使用复制监视器：  
  
-   **sysadmin** 固定服务器角色。  
  
     这些用户可以监视复制，并对更改复制属性（如代理计划、代理配置文件等）拥有完全控制权。  
  
-   分发数据库中的 **replmonitor** 数据库角色。  
  
     这些用户可以监视复制，但不能更改任何复制属性。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **允许非管理员使用复制监视器，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 若要允许非管理员使用复制监视器，属于 **sysadmin** 固定的服务器角色必须将用户添加到分发数据库并向该用户分配 **replmonitor** 角色。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 允许非管理员使用复制监视器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中，连接到分发服务器，然后展开服务器节点。  
  
2.  展开 **数据库**, ，展开 **系统数据库**, ，然后展开分发数据库 (名为 **分发** 默认情况下)。  
  
3.  展开 **安全**, ，用鼠标右键单击 **用户**, ，然后单击 **新用户**。  
  
4.  输入用户名和用户的登录名。  
  
5.  选择默认的 **replmonitor**架构。  
  
6.  在 **“数据库角色成员身份”** 网格中，选中 **“replmonitor”** 复选框。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 将用户添加到 replmonitor 固定数据库角色  
  
1.  在分发数据库上分发服务器上，执行 [sp_helpuser & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)。 如果用户未列在 **用户名** 在结果集中，用户必须授予访问权限的分发数据库 using [CREATE USER & #40;Transact SQL & #41;](../../../t-sql/statements/create-user-transact-sql.md) 语句。  
  
2.  在分发数据库上分发服务器上，执行 [sp_helprolemember & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md), ，将值指定为 **replmonitor** 为 **@rolename** 参数。 如果在结果集中的 **MemberName** 中列出此用户，则此用户已属于此角色。  
  
3.  如果用户不属于 **replmonitor** 角色中，执行 [sp_addrolemember & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) 在分发数据库上分发服务器上。 为 **replmonitor** 参数指定 **参数指定** 并为 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows login being added 参数指定 **指定要添加的数据库用户名称或**。  
  
#### 从 replmonitor 固定数据库角色中删除用户  
  
1.  若要验证用户是否属于 **replmonitor** 角色中，执行 [sp_helprolemember & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) 在分发服务器上分发数据库，并将值指定为 **replmonitor** 为 **@rolename**。 如果在结果集中的 **MemberName** 中未列出此用户，则此用户当前不属于此角色。  
  
2.  如果用户属于 **replmonitor** 角色中，执行 [sp_droprolemember & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) 在分发数据库上分发服务器上。 为 **@rolename** 指定值 **replmonitor** 并为 **@membername**指定要删除的数据库用户名或 Windows 登录名。  
  
  