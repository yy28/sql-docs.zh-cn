---
title: "SQL Server Service Broker | Microsoft Docs"
ms.custom: ""
ms.date: "08/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.SWB.SSBMSGTYPEPROPERTIES.GENERAL.F1"
  - "SQL13.SWB.SSBCONTRACTPROPERTIES.GENERAL.F1"
  - "SQL13.SWB.SSBQUEUEPROPERTIES.GENERAL.F1"
  - "SQL13.SWB.SSBREMSVCBINDPROPERTIES.GENERAL.F1"
  - "SQL13.SWB.SSBROUTEPROPERTIES.GENERAL.F1"
  - "SQL13.SWB.SSBPRIORITYPROPERTIES.GENERAL.F1"
  - "SQL13.SWB.SSBSERVICEPROPERTIES.GENERAL.F1"
helpviewer_keywords: 
  - "Broker，请参阅 Service Broker"
  - "SQL Server Service Broker"
  - "Service Broker"
ms.assetid: 8b8b3b57-fd46-44de-9a4e-e3a8e3999c1e
caps.latest.revision: 22
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 22
---
# SQL Server Service Broker
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSB](../../includes/sssb-md.md)] 为 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 中的消息和队列应用程序提供本机支持。 这使开发人员可以更轻松地创建使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 组件在完全不同的数据库之间进行通信的复杂应用程序。 开发人员可以使用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 轻松生成可靠的分布式应用程序。  
  
 使用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的应用程序开发人员无需编写复杂的内部通信和消息，即可跨多个数据库分发数据工作负荷。 因为 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 会处理会话上下文中的通信路径，所以这就减少了开发和测试工作。 同时还提高了性能。 例如，支持网站的前端数据库可以记录信息，并发送处理密集型任务以便在后端数据库中进行排队。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 确保在事务上下文中管理所有任务，以确保可靠性和技术一致性。  
  
## Service Broker 文档在哪里？  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的参考文档位于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 文档中。 本参考文档包含以下各节：  
  
-   适用于 CREATE, ALTER 和 DROP 语句的[数据定义语言 (DDL) 语句 (Transact-SQL)](../Topic/Data%20Definition%20Language%20\(DDL\)%20Statements%20\(Transact-SQL\).md)  
  
-   [Service Broker 语句](../../t-sql/statements/service-broker-statements.md)  
  
-   [Service Broker 目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)  
  
-   [与 Service Broker 有关的动态管理视图 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
-   [ssbdiagnose 实用工具 (Service Broker)](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
 有关 [概念以及开发和管理任务，请参阅](http://go.microsoft.com/fwlink/?LinkId=231312) 以前发布的文档 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 。 由于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 中的更改数量少，因此未在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]文档中重新生成该文档。  
  
## Service Broker 新增功能  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]未引入任何重大更改。  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中引入了以下更改。  
  
### 可以将消息发送到多个目标服务（多播）  
 通过支持多个会话句柄，扩展了 [SEND (Transact-SQL)](../../t-sql/statements/send-transact-sql.md) 语句的语法以启用多播。  
  
### 队列将公开此消息排队时间  
 队列具有一个新列 **message_enqueue_time**，用于显示消息已在队列中待了多少时间。  
  
### 可以禁用有害消息处理  
 现在，[CREATE QUEUE (Transact-SQL)](../../t-sql/statements/create-queue-transact-sql.md) 和 [ALTER QUEUE (Transact-SQL)](../../t-sql/statements/alter-queue-transact-sql.md) 语句可以通过添加子句 `POISON_MESSAGE_HANDLING (STATUS = ON | OFF)` 来启用或禁用有害消息处理。 目录视图 **sys.service_queues** 现在具有列 **is_poison_message_handling_enabled**，以指示是启用还是禁用有害消息。  
  
### Service Broker 中的 AlwaysOn 支持  
 有关详细信息，请参阅 [Service Broker 与 AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md)。  
  
  