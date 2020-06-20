---
title: 一些可用性副本未同步数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ad89a668a36afa10bbf7b0e35a01226141b0c316
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936448"
---
# <a name="some-availability-replicas-are-not-synchronizing-data"></a>一些可用性副本未同步数据
    
## <a name="introduction"></a>简介  
  
|||  
|-|-|  
|**策略名称**|可用性副本数据同步状态|  
|**问题**|一些可用性副本未同步数据。|  
|**类别**|**警告**|  
|**多**|可用性组 (availability group)|  
  
## <a name="description"></a>说明  
 此策略将汇总可用性组中所有可用性副本的数据同步状态，并且检查是否有可用性副本的同步未执行。 如果可用性副本的任意数据同步状态为 NOT SYNCRONIZING，此策略处于不正常状态。  
  
 如果可用性副本的数据同步状态均不为 NOT SYNCRONIZING，则此策略处于正常状态。  
  
> [!NOTE]  
>  对于此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，与可能原因和解决方法有关的信息位于 TechNet Wiki 上的 [一些可用性副本未同步数据](https://go.microsoft.com/fwlink/p/?LinkId=220852) 中。  
  
## <a name="possible-causes"></a>可能的原因  
 在此可用性组中，至少一个辅助副本具有 NOT SYNCHRONIZING 同步状态，未从主副本接收数据。  
  
## <a name="possible-solution"></a>可能的解决方法  
 使用可用性副本策略状态查找具有 NOT SYNCHROINIZING 状态的可用性副本，然后解决该可用性副本上的问题。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
