---
title: "可用性副本不具有运行状况良好的角色 | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.agdashboard.arp1rolehealthy.issues.f1"
helpviewer_keywords: 
  - "可用性组 [SQL Server], 策略"
ms.assetid: ebb2c9f4-2097-4688-b4fb-8f0571047317
caps.latest.revision: 13
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 13
---
# 可用性副本不具有运行状况良好的角色
    
## 简介  
  
|||  
|-|-|  
|**策略名称**|可用性副本角色状态|  
|**问题**|可用性副本不具有运行状况良好的角色。|  
|**类别**|**严重**|  
|**方面**|可用性副本|  
  
## 说明  
 此策略检查可用性副本的角色的状态。 在可用性副本的角色既不是主副本也不是辅助副本时，该策略将处于不正常状态。 否则，该策略处于正常状态。  
  
> [!NOTE]  
>  对于此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，与可能原因和解决方法有关的信息位于 TechNet Wiki 上的[可用性副本不具有正常角色](http://go.microsoft.com/fwlink/p/?LinkId=220856)中。  
  
## 可能的原因  
 此可用性副本的角色是不正常。 副本既没有主副本角色，也没有辅助副本角色。  
  
## 可能的解决方法：Information_still_to_come  
  
## 另请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  