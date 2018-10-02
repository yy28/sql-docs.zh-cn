---
title: 订阅 - 未分发的命令（事务订阅）| Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6aa7f22cfbc05938b3ff8cf12495fa03b7c8cb4b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813961"
---
# <a name="subscription-undistributed-commands-transactional-subscription"></a>订阅 - 未分发的命令（事务订阅）
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **“未分发的命令”** 选项卡显示分发数据库中尚未传递到所选订阅服务器的命令数的相关信息，以及传递这些命令的估计时间。 有关查看分发数据库中的命令的信息，请参阅 [sp_replshowcmds (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)。  
  
## <a name="options"></a>选项  
 **分发数据库中等待应用于此订阅服务器的命令数**  
 在分发数据库中尚未传递到所选订阅服务器的命令数。 一个命令由一个 Transact-SQL 数据操作语言 (DML) 语句或一个数据定义语言 (DDL) 语句组成。  
  
 **根据过去的性能估计应用这些命令所需的时间为**  
 将命令传递到订阅服务器所需的估计时间。 如果此值大于生成快照并将其应用于订阅服务器所需的时间，请考虑重新初始化订阅服务器。 有关详细信息，请参阅 [重新初始化订阅](../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [使用复制监视器监视性能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [监视复制](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
