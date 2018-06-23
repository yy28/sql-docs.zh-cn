---
title: 跟踪模板属性 （事件选择选项卡） |Microsoft 文档
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
- sql12.pro.tracetemplateproperties.eventsselection.f1
helpviewer_keywords:
- Trace Template Properties dialog box
ms.assetid: 5b202457-ab42-4902-8012-7f3f40aa09f5
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 097772336c66b6b1832a6e0bb16791fc107ec81a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017419"
---
# <a name="trace-template-properties-events-selection-tab"></a>跟踪模板属性（“事件选择”选项卡）
  使用 **“跟踪模板属性”** 对话框的 **“事件选择”** 选项卡，可以查看、编辑或指定要包含在 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 跟踪模板中的事件类和数据列。  
  
## <a name="options"></a>“常规”  
 “事件”列  
 通过选择或清除事件列中的复选框，指定要跟踪的事件。 事件按事件类别进行组织。  
  
 如果在 **“常规”** 选项卡上选中 **“使新模板基于现有模板”** ，将会根据指定的模板自动选择事件。 有关事件类的详细信息，请参阅 [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
 数据列  
 通过选中与所需的事件和数据列对应的框，指定要跟踪的数据列。 如果选中与事件对应的复选框，则默认情况下，将选中与跟踪中包括的每一个事件相关的事件列。 如果在 **“常规”** 选项卡上选中 **“使新模板基于现有模板”** ，将会根据指定的模板自动选择数据列和筛选器。  
  
 通过单击数据列标题并输入筛选条件指定筛选器。 筛选出来的数据列由 **“编辑筛选器”** 对话框中列标签左边的筛选器图标指示。  
  
 **显示所有事件**  
 显示所有可用事件。 如果创建的新模板不是基于现有模板，默认情况下将选中此选项。 取消选中该复选卡可以隐藏 **“事件选择”** 网格中所有未选定的事件。  
  
 **显示所有列**  
 显示所有可用数据列。 如果创建的新模板不是基于现有模板，默认情况下将选中此选项。 取消选中该复选卡可以隐藏 **“事件选择”** 网格中所有未选定的数据列。  
  
 **列筛选器**  
 启动“编辑筛选器”对话框，该对话框将在数据列标签的左侧显示一个筛选器图标。 使用 **“编辑筛选器”** 对话框可编辑数据列筛选器。  
  
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
  
  