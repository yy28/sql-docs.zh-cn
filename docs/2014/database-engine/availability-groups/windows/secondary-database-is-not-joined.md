---
title: 未联接辅助数据库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.drp2joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 10817e5e-75fa-42dd-baa2-359bea3ad051
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68bb7821417f0bb4560f4371c3baa16c6ecf77d7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135007"
---
# <a name="secondary-database-is-not-joined"></a>未联接辅助数据库
    
## <a name="introduction"></a>简介  
  
|||  
|-|-|  
|**策略名称**|可用性数据库联接状态|  
|**问题**|未联接辅助数据库。|  
|**类别**|**警告**|  
|**方面**|可用性数据库|  
  
## <a name="description"></a>Description  
 此策略检查辅助数据库（也称为“辅助数据库副本”）的联接状态。 数据集副本未联接时，此策略处于不正常状态。 否则，该策略处于正常状态。  
  
> [!NOTE]  
>  对于此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，与可能原因和解决方法有关的信息位于 TechNet Wiki 上的 [未联接辅助数据库](http://go.microsoft.com/fwlink/p/?LinkId=220862) 中。  
  
## <a name="possible-causes"></a>可能的原因  
 此辅助数据库未联接到可用性组。 此辅助数据库的配置不完整。  
  
## <a name="possible-solution"></a>可能的解决方法  
 使用 Transact-SQL、PowerShell 或 SQL Server Management Studio 将辅助副本联接到可用性组。 有关将辅助副本联接到可用性组的详细信息，请参阅 [将辅助副本联接到可用性组 (SQL Server)](http://msdn.microsoft.com/en-sg/library/ff878473\(en-us,SQL.110\).aspx)。  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
