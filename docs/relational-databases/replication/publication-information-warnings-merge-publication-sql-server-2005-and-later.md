---
title: "发布信息，警告（合并发布，SQL Server 2005 及更高版本） | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publicationinfo.warningsandagents.merge.f1"
ms.assetid: 9bef3565-5f13-42ac-8723-ebe55b0c11e6
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# 发布信息，警告（合并发布，SQL Server 2005 及更高版本）
  **“警告”** 选项卡适用于运行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本的分发服务器。 使用 **“警告”** 选项卡可以为所选发布执行下列任务：  
  
-   启用警告。  
  
-   指定与警告关联的阈值。  
  
-   定义与警告关联的警报。  
  
## 警告、阈值和警报  
 默认情况下，复制监视器会为未初始化的订阅显示警告：在包含订阅信息的页的 **“状态”** 列中，显示 **“未初始化的订阅”** 状态作为警告。 对于合并发布，可以指定以下附加条件是否导致警告：  
  
-   订阅即将过期。  
  
     它对应于选项 **“如果订阅将在阈值内过期，则发出警告”**。 如果达到或超过指定的阈值，订阅状态将显示为 **即将过期/已过期** （除非需要显示具有较高优先级的问题）。  
  
-   超出了指定的同步时间。  
  
     它对应于选项 **“如果拨号连接的合并长度超出阈值，则发出警告”** 和 **“如果 LAN 连接的合并长度超出阈值，则发出警告”**。 可以设置这两个阈值，但在给定的同步过程中仅使用其中的一个。 合并代理将根据连接类型来应用相应的阈值。  
  
     如果达到或超过指定的阈值，订阅状态将显示为 **长时间运行的合并** （除非需要显示具有较高优先级的问题）。  
  
-   在给定时间内未处理完指定的行数。  
  
     它对应于选项 **“如果拨号连接每秒合并的行数小于阈值，则发出警告”** 和 **“如果 LAN 连接的合并长度超出阈值，则发出警告”**。 可以设置这两个阈值，但在给定的同步过程中仅使用其中的一个。 合并代理将根据连接类型来应用相应的阈值。  
  
     如果达到或超过指定的阈值，订阅状态将显示为 **性能关键** （除非需要显示具有较高优先级的问题）。  
  
 启用警告时，还需要设置阈值。 例如，如果启用警告 **“如果 LAN 连接的合并长度超出阈值，则发出警告”**，请设置合并同步允许的最大时间长度。  
  
 除了在复制监视器中显示警告之外，达到阈值也可以触发警报。 通过单击 **“配置警报”** 并在 **“配置复制警报”** 对话框中提供信息，可以定义警报。  
  
## 选项  
 **已启用**  
 选择此项可以启用警告并指定阈值。  
  
 **警报**  
 选择可启用给定复制警报的警报设置。  
  
 **警告**  
 与阈值关联的警告的说明。  
  
 **阈值**  
 指定阈值的值。  
  
 **配置警报**  
 选择中的某一行 **警告** 网格中，然后单击 **配置警报** 启动 **配置复制警报** 对话框。 使用该对话框，可以定义与所选阈值和警告关联的警报。  
  
 **放弃更改**  
 单击此项可放弃对警告和阈值所做的任何更改。  
  
> [!NOTE]  
>  单击 **放弃更改** 不会影响在定义的警报 **配置复制警报** 对话框。  
  
 **保存更改**  
 单击此项可保存对警告和阈值所做的任何更改。  
  
## 另请参阅  
 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [查看信息并执行任务发布 & #40;复制监视器 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [用复制监视器监视性能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [监视复制](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [在复制监视器中设置阈值和警告](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  