---
title: 活动监视器 | Microsoft Docs
description: 了解如何使用活动监视器显示有关 SQL Server 进程的信息以及这些进程如何影响 SQL Server 的当前实例。
ms.custom: ''
ms.date: 04/07/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server]
ms.assetid: 1e6c430d-3a2a-468e-a3d5-ef5459c36c15
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: ad03ee3c5c9cc0128bb281ff695c1f51cc518d6e
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457767"
---
# <a name="activity-monitor"></a>活动监视器
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
活动监视器显示有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的信息，并了解这些进程如何影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的当前实例。  
  
活动监视器是一个带有以下可展开和折叠的窗格的选项卡式文档窗口：“概述”、“进程”、“资源等待”、“数据文件 I/O”、“最近耗费大量资源的查询”和“耗费大量资源的活动查询”。 展开任何窗格时，活动监视器都将查询实例以获取相关信息。 折叠窗格时，该窗格的所有查询活动都将停止。 你可以同时展开一个或多个窗格，以查看实例上不同种类的活动。  
 
## <a name="customize-columns"></a>自定义列 
对于在“进程”、“资源等待”、“数据文件 I/O”、“最近耗费大量资源的查询”和“耗费大量资源的活动查询”窗格中的列，用以下方式自定义显示内容：  
  
1.  若要重排列的顺序，请单击列标题，并将其拖到标题功能区中的另一位置。  
  
2.  若要排序列，请单击列名称。  
  
3.  若要对一个或多个列进行筛选，请单击列标题中的下拉箭头，然后选择值。  

## <a name="more-information"></a>详细信息  
   
|||  
|-|-|  
|说明如何打开活动监视器和如何设置活动监视器刷新间隔。|[打开活动监视器 (SQL Server Management Studio)](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)|  
|链接到关于服务器性能和活动监视的主题。|[服务器性能和活动监视](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|  
  
  
