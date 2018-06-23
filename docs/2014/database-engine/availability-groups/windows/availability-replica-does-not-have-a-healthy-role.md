---
title: 可用性副本不具有运行状况良好的角色 | Microsoft Docs
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
- sql12.swb.agdashboard.arp1rolehealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: ebb2c9f4-2097-4688-b4fb-8f0571047317
caps.latest.revision: 11
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 4a27027a499e37ace19892f030802bbf5b143687
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124403"
---
# <a name="availability-replica-does-not-have-a-healthy-role"></a>可用性副本不具有运行状况良好的角色
    
## <a name="introduction"></a>简介  
  
|||  
|-|-|  
|**策略名称**|可用性副本角色状态|  
|**问题**|可用性副本不具有运行状况良好的角色。|  
|**类别**|**严重**|  
|**方面**|可用性副本|  
  
## <a name="description"></a>Description  
 此策略检查可用性副本的角色的状态。 在可用性副本的角色既不是主副本也不是辅助副本时，该策略将处于不正常状态。 否则，该策略处于正常状态。  
  
> [!NOTE]  
>  对于此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，与可能原因和解决方法有关的信息位于 TechNet Wiki 上的 [可用性副本不具有正常角色](http://go.microsoft.com/fwlink/p/?LinkId=220856) 中。  
  
## <a name="possible-causes"></a>可能的原因  
 此可用性副本的角色是不正常。 副本既没有主副本角色，也没有辅助副本角色。  
  
## <a name="possible-solution-informationstilltocome"></a>可能的解决方法：Information_still_to_come  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  