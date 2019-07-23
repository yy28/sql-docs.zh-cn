---
title: 可用性副本不具有用于可用性组的运行状况良好的角色
description: 确定在 Always On 可用性组中副本不具有运行状况良好的角色的可能原因。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.arp1rolehealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: ebb2c9f4-2097-4688-b4fb-8f0571047317
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9454b48f17af904db87e0000b07651c1bc454362
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991381"
---
# <a name="availability-replica-does-not-have-a-healthy-role-for-an-always-on-availability-group"></a>可用性副本不具有用于 Always On 可用性组的运行状况良好的角色
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>简介  
  
|||  
|-|-|  
|**策略名称**|可用性副本角色状态|  
|**问题**|可用性副本不具有运行状况良好的角色。|  
|**类别**|**严重**|  
|**方面**|可用性副本|  
  
## <a name="description"></a>描述  
 此策略检查可用性副本的角色的状态。 在可用性副本的角色既不是主副本也不是辅助副本时，该策略将处于不正常状态。 否则，该策略处于正常状态。  
  
> [!NOTE]  
>  对于此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，与可能原因和解决方法有关的信息位于 TechNet Wiki 上的 [可用性副本不具有正常角色](https://go.microsoft.com/fwlink/p/?LinkId=220856) 中。  
  
## <a name="possible-causes"></a>可能的原因  
 此可用性副本的角色是不正常。 副本既没有主副本角色，也没有辅助副本角色。  
  
## <a name="possible-solution-informationstilltocome"></a>可能的解决方法：Information_still_to_come  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
