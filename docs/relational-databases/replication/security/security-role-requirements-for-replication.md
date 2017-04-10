---
title: "复制的安全角色要求 | Microsoft Docs"
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
  - "安全性 [SQL Server 复制], 角色"
  - "角色 [SQL Server], 复制"
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 复制的安全角色要求
  复制限制用户以用户登录名映射到的角色执行的特定操作。 复制已授予特定权限 **sysadmin** 固定服务器角色、 **db_owner** 固定数据库角色以及登录名在发布访问列表 (PAL) 中。  
  
## 复制设置的安全角色要求  
 下表概述了常见复制设置任务所需的身份验证级别：  
  
|设置任务|成员身份要求|  
|----------------|----------------------------|  
|启用分发服务器、发布服务器或订阅服务器。|发布服务器上的**sysadmin** 服务器角色。|  
|启用数据库进行复制。|发布服务器上的**sysadmin** 服务器角色。|  
|创建发布。|**db_owner** 发布服务器上的发布数据库上的数据库角色或 **sysadmin** 发布服务器上的服务器角色。|  
|查看发布属性。|在发布服务器上的 PAL 成员 **db_owner** 在发布服务器上的发布数据库上的数据库角色或 **sysadmin** 发布服务器上的服务器角色。|  
|创建订阅。|**db_owner** 发布服务器上的发布数据库上的数据库角色或 **sysadmin** 发布服务器上的服务器角色。<br /><br /> **db_owner** 订阅服务器上的订阅数据库上的数据库角色或 **sysadmin** 订阅服务器上的服务器角色。|  
|配置代理配置文件。|分发服务器上的**sysadmin** 服务器角色。|  
  
## 复制维护的安全角色要求  
 下表概述了常见复制维护任务所需的身份验证级别：  
  
|维护任务|成员身份要求|  
|----------------------|----------------------------|  
|修改或删除分发服务器、发布服务器或订阅服务器。|相应服务器上的**sysadmin** 服务器角色。|  
|修改或删除发布。|**db_owner** 发布服务器上的发布数据库上的数据库角色或 **sysadmin** 发布服务器上的服务器角色。|  
|修改或删除发布服务器上的订阅。|**db_owner** 发布服务器上的发布数据库上的数据库角色或 **sysadmin** 发布服务器上的服务器角色。|  
|修改或删除订阅服务器上的订阅。|**db_owner** 订阅服务器上的订阅数据库上的数据库角色或 **sysadmin** 订阅服务器上的服务器角色。|  
|将订阅标记为要重新初始化。|推送订阅︰ **db_owner** 发布服务器上对发布数据库中的数据库角色或 **sysadmin** 发布服务器上的服务器角色。<br /><br /> 请求订阅︰ **db_owner** 订阅服务器上的订阅数据库中的数据库角色或 **sysadmin** 订阅服务器上的服务器角色。|  
|使用复制监视器查看复制活动、错误和历史记录。 用户不能修改代理配置文件、计划等，除非用户是 **sysadmin** 服务器角色成员。|分发服务器的分发数据库上的**replmonitor** 数据库角色或分发服务器上的 **sysadmin** 服务器角色。|  
|维护复制代理。|**db_owner** 中相应的数据库的数据库角色或 **sysadmin** 适当的服务器上的服务器角色。<br /><br /> 如果代理是由 **sysadmin** 角色中的用户创建的，并且未给该代理指定代理帐户，则该代理将在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理帐户上下文运行。 在这种情况下，用户中 **db_owner** 角色不能修改与代理关联的作业。|  
|启动或停止复制代理。|代理作业的所有者或相应服务器上的 **sysadmin** 服务器角色。|  
  
## 另请参阅  
 [复制安全最佳实践](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全和保护与 #40;复制和 #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  