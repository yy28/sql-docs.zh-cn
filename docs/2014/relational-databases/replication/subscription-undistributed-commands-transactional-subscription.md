---
title: 订阅-未分发的命令 （事务订阅，SQL Server 2005 和更高版本） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 88124bde6d1f8b54a875f1c30076408dc24fcc2c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238708"
---
# <a name="subscription-undistributed-commands-transactional-subscription-sql-server-2005-and-later"></a>订阅，未分发的命令（事务订阅，SQL Server 2005 和更高版本）
  **“未分发的命令”** 选项卡显示分发数据库中尚未传递到所选订阅服务器的命令数的相关信息，以及传递这些命令的估计时间。 有关查看分发数据库中的命令的信息，请参阅 [sp_replshowcmds (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql)。  
  
## <a name="options"></a>“常规”  
 **分发数据库中等待应用于此订阅服务器的命令数**  
 在分发数据库中尚未传递到所选订阅服务器的命令数。 一个命令由一个 Transact-SQL 数据操作语言 (DML) 语句或一个数据定义语言 (DDL) 语句组成。  
  
 **根据过去的性能估计应用这些命令所需的时间为**  
 将命令传递到订阅服务器所需的估计时间。 如果此值大于生成快照并将其应用于订阅服务器所需的时间，请考虑重新初始化订阅服务器。 有关详细信息，请参阅 [重新初始化订阅](reinitialize-subscriptions.md)。  
  
## <a name="see-also"></a>请参阅  
 [启动复制监视器](monitor/start-the-replication-monitor.md)   
 [使用复制监视器监视性能](monitor/monitor-performance-with-replication-monitor.md)   
 [监视复制](monitoring-replication.md)  
  
  
