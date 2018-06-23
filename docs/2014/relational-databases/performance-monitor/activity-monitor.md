---
title: 活动监视器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Activity Monitor [SQL Server]
ms.assetid: 1e6c430d-3a2a-468e-a3d5-ef5459c36c15
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 683e1c41e6f0edb45cd7c0da1b52622818d441b9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017725"
---
# <a name="activity-monitor"></a>活动监视器
  活动监视器显示有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的信息，并了解这些进程如何影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的当前实例。  
  
## <a name="benefits-of-activity-monitor"></a>活动监视器的优点  
 活动监视器是一个具有以下可展开和折叠窗格的选项卡式的文档窗口：**概述**，**活动用户任务**，**资源等待**， **数据文件 I/O**，和**最近昂贵的查询**。 展开任何窗格时，活动监视器都将查询实例以获取相关信息。 折叠窗格时，该窗格的所有查询活动都将停止。 还可以同时展开一个或多个窗格，以查看实例上不同种类的活动。  
  
 中包含的列**活动用户任务**，**资源等待**，**数据文件 I/O**，和**最近昂贵的查询**窗格中，你可以自定义显示通过以下方式：  
  
1.  若要重排列的顺序，请单击列标题，并将其拖到标题功能区中的另一位置。  
  
2.  若要排序列，请单击列名称。  
  
3.  若要对一个或多个列进行筛选，请单击列标题中的下拉箭头，然后选择值。  
  
## <a name="related-tasks"></a>Related Tasks  
 通过以下任务以开始使用活动监视器：  
  
|||  
|-|-|  
|**Description**|**主题**|  
|说明如何打开活动监视器和如何设置活动监视器刷新间隔。|[打开活动监视器 (SQL Server Management Studio)](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)|  
|链接到关于服务器性能和活动监视的主题。|[服务器性能和活动监视](../performance/server-performance-and-activity-monitoring.md)|  
  
  