---
title: 跟踪表属性 （事件选择选项卡） |Microsoft 文档
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
- sql12.pro.tracetableproperties.eventsselection.f1
helpviewer_keywords:
- Trace Table Properties dialog box
ms.assetid: fa21df6a-b6b5-4b15-9104-957385821594
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 503c7851b79135fa2c4d4a0dc6888c7345414ea9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014600"
---
# <a name="trace-table-properties-events-selection-tab"></a>跟踪表属性（“事件选择”选项卡）
  使用 **“跟踪表属性”** 对话框的 **“事件选择”** 选项卡可以查看跟踪的事件和数据列属性，或者从跟踪中删除事件或列。  
  
 若要查看此窗口，请使用 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 打开一个跟踪表。 然后在 **“文件”** 菜单上单击 **“属性”**，再单击 **“事件选择”** 选项卡。  
  
## <a name="options"></a>“常规”  
 “事件”列  
 查看按事件类别组织的跟踪事件。 可以通过选中事件框或选中事件的数据列来选择事件。 如果选中事件框，则该事件的所有可用数据列均被选中。 如果选中了某个事件的数据列，则该事件将被选中，并且其他所有必需列也被自动选中。 如果您正在查看跟踪文件或表，清除事件复选框或数据列将减少跟踪窗口中的可见数据量，便于分析。 您也可以更改列筛选器以减少跟踪窗口中的可见数据量。 有关事件类的详细信息，请参阅 [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
 其他数据列  
 查看跟踪数据列。 默认情况下，将会为跟踪中包含的每个事件选中跟踪中的所有相关数据列。  
  
 通过单击数据列标题并输入筛选条件指定筛选器。 筛选出来的数据列由 **“编辑筛选器”** 对话框中列标签左边的筛选器图标指示。  
  
 **显示所有事件**  
 显示所有可用事件。 默认情况下，仅显示 **“事件选择”** 网格中选定的行。 取消选中此框，将隐藏 **“事件选择”** 网格中所有未选定的事件。 如果选中了 **“显示所有事件”** ，并且您正在查看跟踪文件或表，则跟踪过程中记录的所有事件都将显示在跟踪窗口中。  
  
 **显示所有列**  
 显示所有可用数据列。 默认情况下，仅显示选定的数据列。 取消选中此框，将隐藏 **“事件选择”** 网格中所有未选定的数据列。  
  
 **列筛选器**  
 启动“编辑筛选器”对话框，该对话框在列标签的左侧显示一个筛选器图标。 您可以使用此对话框编辑数据列筛选器。  
  
 **组织列**  
 选择要跟踪的**事件**和数据列后，单击“组织列”将强制网格对跟踪结果窗口中的列重新排序。  
  
## <a name="see-also"></a>请参阅  
 [打开跟踪表 (SQL Server Profiler)](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler 模板和权限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server 事件探查器](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  