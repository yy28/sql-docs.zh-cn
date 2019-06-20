---
title: 设置 SQL Server 数据库警报 (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3342af1de84e922ce63848c8fdffe5aa30ec309a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150501"
---
# <a name="set-up-a-sql-server-database-alert-windows"></a>设置 SQL Server 数据库警报 (Windows)
  通过使用系统监视器可以创建一个在达到系统监视器计数器的阈值时发出的警报。 作为对警报的响应，系统监视器会启动一个应用程序，例如为处理警报情况而编写的自定义应用程序。 例如，您可以创建在死锁数超过特定值时将会引发的警报。  
  
 此外，还可以使用 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理来定义警报。 有关详细信息，请参阅 [“警报”](../../ssms/agent/alerts.md)。  
  
### <a name="to-set-up-a-sql-server-database-alert"></a>设置 SQL Server 数据库警报  
  
1.  在“性能”窗口的导航树中，展开 **“性能日志和警报”** 。  
  
2.  右键单击“警报”  ，再单击“新建警报设置”  。  
  
3.  在 **“新建警报设置”** 对话框中，输入新警报的名称，再单击 **“确定”** 。  
  
4.  在新建警报对话框的 **“常规”** 选项卡上，添加一个 **注释**，再单击 **“添加”** 为该警报添加计数器。  
  
     所有警报必须至少有一个计数器。  
  
5.  在“添加计数器”对话框中，从 **“性能对象”** 列表选择一个 SQL Server 对象，然后从 **“从列表中选择计数器”** 选择一个计数器。  
  
6.  若要为警报添加计数器，请单击 **“添加”** 。 您可以继续添加计数器，也可以单击 **“关闭”** 返回到新建警报对话框。  
  
7.  在新建警报对话框的“将触发警报，如果值是：”  列表中，单击“超过”  或“低于”  ，然后在“限制”  中输入一个阈值。  
  
     当计数器的值大于或小于阈值时（取决于单击的是“超过”  还是“低于”  ），将生成警报。  
  
8.  在 **“数据采样间隔”** 框中，设置采样频率。  
  
9. 在 **“操作”** 选项卡上，设置每次触发警报时要执行的操作。  
  
10. 在 **“计划”** 选项卡上，设置警报扫描的开始和停止计划。  
  
## <a name="see-also"></a>请参阅  
 [创建 SQL Server 数据库警报](../performance-monitor/create-a-sql-server-database-alert.md)  
  
  
