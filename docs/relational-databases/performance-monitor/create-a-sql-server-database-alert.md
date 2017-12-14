---
title: "创建 SQL Server 数据库警报 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database performance [SQL Server], alerts
- alerts [SQL Server], creating
- thresholds [SQL Server]
- database alerts [SQL Server]
- tuning databases [SQL Server], alerts
- monitoring performance [SQL Server], alerts
- monitoring server performance [SQL Server], alerts
- database monitoring [SQL Server], alerts
- server performance [SQL Server], alerts
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ede030243e026922d5e3d2ff8774fd6264e45e2f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-sql-server-database-alert"></a>创建 SQL Server 数据库警报
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]可以使用系统监视器创建一个在达到系统监视器计数器的阈值时发出的警报。 系统监视器将启动一个应用程序（例如，为处理警报情况而编写的自定义应用程序）来响应警报。 例如，可以创建一个在死锁数超过特定值时发出的警报。  
  
 此外，还可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理来定义警报。 有关详细信息，请参阅 [“警报”](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef)。  
  
 有关使用系统监视器设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库警报的详细信息，请参阅[设置 SQL Server 数据库警报 (Windows)](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md)。  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_alert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sys.sysperfinfo (Transact-SQL)](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  
