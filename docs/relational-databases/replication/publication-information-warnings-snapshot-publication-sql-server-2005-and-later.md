---
title: 警告（快照 - 复制监视器）
decription: Describes the 'Warnings' tab for a Snapshot Publication in the Replication Monitor found in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.warningsandagents.snapshot.f1
ms.assetid: 7aa2eb52-b6b7-4dd3-8483-8ef00d9f0435
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: e23c798722928a8374dae43002ba44ca0347c76a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720928"
---
# <a name="publication-information-warnings-snapshot-publication-sql-server-2005-and-later"></a>发布信息，警告（快照发布，SQL Server 2005 及更高版本）
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **“警告”** 选项卡适用于运行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本的分发服务器。 使用 **“警告”** 选项卡可以为所选发布执行下列任务：  
  
-   启用警告。  
  
-   指定与警告关联的阈值。  
  
-   定义与警告关联的警报。  
  
## <a name="warnings-thresholds-and-alerts"></a>警告、阈值和警报  
 默认情况下，复制监视器会为未初始化的订阅显示警告：在包含订阅信息的页的 **“状态”** 列中，显示 **“未初始化的订阅”** 状态作为警告。 对于快照发布，您也可以通过设置选项 **“如果订阅将在阈值内过期，则发出警告”** ，指定在订阅即将过期时发出警告。 如果达到或超过指定的阈值，订阅状态将显示为 **“即将过期/已过期”** （除非需要显示更高优先级的问题）。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [使用复制监视器查看信息和执行任务](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [监视复制](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
