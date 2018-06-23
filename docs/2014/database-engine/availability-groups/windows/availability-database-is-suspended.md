---
title: 可用性数据库挂起 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.agdashboard.drp1notsuspended.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6baee70f-848c-4e86-b20d-78875c0f82cb
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 6ff9d79ede6794d1242a7ad743f1a29d279183ea
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027982"
---
# <a name="availability-database-is-suspended"></a>可用性数据库挂起
    
## <a name="introduction"></a>简介  
  
|||  
|-|-|  
|**策略名称**|可用性数据库挂起状态|  
|**问题**|可用性数据库挂起。|  
|**类别**|**警告**|  
|**方面**|可用性数据库|  
  
## <a name="description"></a>Description  
 此策略检查辅助数据库（也称为“辅助数据库副本”）的数据移动状态。 数据移动挂起时，此策略处于不正常状态。 否则，该策略处于正常状态。  
  
> [!NOTE]  
>  对于此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，与可能原因和解决方法有关的信息位于 [TechNet Wiki 上的可用性数据库挂起](http://go.microsoft.com/fwlink/p/?LinkId=220860) 中。  
  
## <a name="possible-causes"></a>可能的原因  
 由于下列原因，此可用性数据库上的数据同步可能已挂起：  
  
-   由于错误，系统可能已挂起数据同步。  
  
-   数据库管理员出于维护目的可能已挂起数据同步。  
  
## <a name="possible-solution"></a>可能的解决方法  
 继续数据同步。 如果问题仍然存在，请在事件日志中查看该可用性组，然后诊断系统挂起数据移动的原因。  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  