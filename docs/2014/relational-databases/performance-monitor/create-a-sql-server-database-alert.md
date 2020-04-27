---
title: 创建 SQL Server 数据库警报 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7c95605ed1a0ab42340713c5c5fa635b09d4a8ab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63249482"
---
# <a name="create-a-sql-server-database-alert"></a>创建 SQL Server 数据库警报
  可以使用系统监视器创建一个在达到系统监视器计数器的阈值时发出的警报。 系统监视器将启动一个应用程序（例如，为处理警报情况而编写的自定义应用程序）来响应警报。 例如，可以创建一个在死锁数超过特定值时发出的警报。  
  
 此外，还可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理来定义警报。 有关详细信息，请参阅 [“警报”](../../ssms/agent/alerts.md)。  
  
 有关使用系统监视器设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库警报的详细信息，请参阅[设置 SQL Server 数据库警报 (Windows)](../performance/set-up-a-sql-server-database-alert-windows.md)。  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_alert (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)   
 [sys.sysperfinfo (Transact-SQL)](/sql/relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql)  
  
  
