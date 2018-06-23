---
title: 跟踪属性 （事件选择选项卡） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.pro.traceproperties.eventsselection.f1
helpviewer_keywords:
- Trace Properties dialog box
ms.assetid: e1892f24-7272-4d5d-8926-6150cc82b2c3
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 627785dc9be7d6b2d270d82f1bc6797c98980779
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124398"
---
# <a name="trace-properties-events-selection-tab"></a>跟踪属性（“事件选择”选项卡）
  使用 **“跟踪属性”** 对话框的 **“事件选择”** 选项卡可以查看或指定跟踪的事件和数据列。  
  
## <a name="options"></a>“常规”  
 “事件”列  
 通过选中或清除事件列中的复选框，指定跟踪的事件。 **“事件”** 按事件类别进行组织。 模板中指定的事件类是自动选择的。 有关详细信息，请参阅 [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
 数据列  
 通过选中与所需的事件和数据列对应的框，指定跟踪的数据列。 对于在跟踪中包括的每个事件，将默认选中所有相关事件列。  
  
 通过单击数据列标题并输入筛选条件指定筛选器。 筛选出来的数据列由 **“编辑筛选器”** 对话框中列标签左边的筛选器图标指示。 有关详细信息，请参阅 [SQL Server Profiler - 编辑筛选器](../../2014/database-engine/sql-server-profiler-edit-filter.md)。  
  
 **显示所有事件**  
 显示所有可用事件。 默认情况下，仅显示 **“事件选择”** 网格中选定的行。 取消选中此框，将隐藏 **“事件选择”** 网格中所有未选定的事件。  
  
 **显示所有列**  
 显示所有可用数据列。 默认情况下，仅显示选定的数据列。 取消选中此框，将隐藏 **“事件选择”** 网格中所有未选定的数据列。  
  
 **列筛选器**  
 启动“编辑筛选器”对话框。 您可以使用此对话框编辑数据列筛选器。  
  
 **组织列**  
 更改跟踪中列的顺序，并按一列或多列对结果分组。  
  
## <a name="see-also"></a>请参阅  
 [指定跟踪文件的事件和数据列&#40;SQL Server 事件探查器&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [组织跟踪中显示的列&#40;SQL Server 事件探查器&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [在跟踪中筛选事件&#40;SQL Server 事件探查器&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [查看筛选器信息 (SQL Server Profiler)](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [修改筛选器&#40;SQL Server 事件探查器&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [SQL Server Profiler 模板和权限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server 事件探查器](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  