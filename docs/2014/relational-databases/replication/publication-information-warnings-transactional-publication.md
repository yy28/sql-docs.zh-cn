---
title: 发布信息-警告 （事务发布，SQL Server 2005 和更高版本） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.warningsandagents.tran.f1
ms.assetid: 4d4baf1d-d0a1-4d09-bec7-137811f43f09
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e2ab1c4be29b87e1051daa702ce40905a95e34ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63022001"
---
# <a name="publication-information-warnings-transactional-publication-sql-server-2005-and-later"></a>发布信息，警告（事务发布，SQL Server 2005 及更高版本）
  **“警告”** 选项卡适用于运行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本的分发服务器。 使用 **“警告”** 选项卡可以为所选发布执行下列任务：  
  
-   在复制监视器中显示警告。  
  
-   指定与警告关联的阈值。  
  
-   定义与警告关联的警报。  
  
## <a name="warnings-thresholds-and-alerts"></a>警告、阈值和警报  
 默认情况下，复制监视器会为未初始化的订阅显示警告：在包含订阅信息的页的 **“状态”** 列中，显示 **“未初始化的订阅”** 状态作为警告。 对于事务发布，您可以指定下列这些附加条件是否会导致警告：  
  
-   订阅即将过期。  
  
     它对应于选项 **“如果订阅将在阈值内过期，则发出警告”**。 如果达到或超过指定的阈值，订阅状态将显示为 **“即将过期/已过期”** （除非需要显示更高优先级的问题）。  
  
-   超出指定的滞后时间。 这是从在发布服务器提交事务到在订阅服务器提交对应的事务所经过的时间。  
  
     它对应于选项 **“如果滞后时间超出阈值，则发出警告”**。 如果达到或超过指定的阈值，订阅状态将显示为 **“‘严重’状态下的性能”** （除非需要显示更高优先级的问题）。 该阈值还可用于确定性能等级，等级信息显示在包含订阅信息的页上的 **“性能”** 列中。 性能等级可以为以下值之一：  
  
    -   很好  
  
    -   好  
  
    -   一般  
  
    -   较差  
  
    -   严重  
  
 启用警告时，还需要设置阈值。 例如，如果启用警告 **“如果滞后时间超出阈值，则发出警告”**，请选择在发布服务器上提交事务与在订阅服务器上提交事务之间允许的时间间隔。  
  
 除了在复制监视器中显示警告之外，达到阈值也可以触发警报。 通过单击 **“配置警报”** 并在 **“配置复制警报”** 对话框中提供信息，可以定义警报。  
  
## <a name="options"></a>选项  
 **已启用**  
 选择此项可以启用警告并指定阈值。  
  
 **警告**  
 与阈值关联的警告的说明。  
  
 **阈值**  
 指定阈值的值。  
  
 **“配置警报”**  
 从 **“警告”** 网格中选择行，再单击 **“配置警报”** 可启动 **“配置复制警报”** 对话框。 使用该对话框，可以定义与所选阈值和警告关联的警报。  
  
 **放弃更改**  
 单击此项可放弃对警告和阈值所做的任何更改。  
  
> [!NOTE]  
>  单击 **“放弃更改”** 不会影响在 **“配置复制警报”** 对话框中定义的警报。  
  
 **保存更改**  
 单击此项可保存对警告和阈值所做的任何更改。  
  
## <a name="see-also"></a>请参阅  
 [启动复制监视器](monitor/start-the-replication-monitor.md)   
 [使用复制监视器查看信息和执行任务](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [使用复制监视器监视性能](monitor/monitor-performance-with-replication-monitor.md)   
 [监视复制](monitoring-replication.md)   
 [Set Thresholds and Warnings in Replication Monitor](monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
