---
title: 跟踪文件属性 （事件选择选项卡） |Microsoft 文档
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
- sql12.pro.tracefileproperties.eventsselection.f1
helpviewer_keywords:
- Trace File Properties dialog box
ms.assetid: 158d442f-2225-4173-8545-fb1cf611b4d0
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fdc365671beae3d0037ca9f3dca9b0c2a1f21ad4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129724"
---
# <a name="trace-file-properties-events-selection-tab"></a>跟踪文件属性（“事件选择”选项卡）
  使用 **“跟踪文件模板属性”** 对话框的 **“事件选择”** 选项卡，可以查看跟踪的列属性或者从跟踪中删除数据列。  
  
 若要查看此窗口，请打开跟踪文件。 然后，在 **“文件”** 菜单上，单击 **“属性”**，再单击 **“事件选择”** 选项卡。  
  
## <a name="options"></a>“常规”  
 “事件”列  
 查看按事件类别组织的跟踪事件。 最初，跟踪中的所有事件均被选中。 可以通过选中事件框或选中事件的数据列来选择事件。 如果选中事件框，则该事件的所有可用数据列均被选中。 如果选中了某个事件的数据列，则该事件将被选中，并且其他所有必需列也被自动选中。 如果您正在查看跟踪文件或表，清除事件复选框或数据列将减少跟踪窗口中的可见数据量，便于分析。 您也可以更改列筛选器以减少跟踪窗口中的可见数据量。 有关事件类的详细信息，请参阅 [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
 数据列  
 查看跟踪数据列。 默认情况下，将会为跟踪中包含的每个事件选中跟踪中的所有相关数据列。  
  
 通过单击数据列标题并输入筛选条件指定筛选器。 筛选出来的数据列由 **“编辑筛选器”** 对话框中列标签左边的筛选器图标指示。  
  
 **显示所有事件**  
 显示所有可用事件。 默认情况下，仅显示 **“事件选择”** 网格中选定的行。 取消选中此框，将隐藏 **“事件选择”** 网格中所有未选定的事件。 如果选中了 **“显示所有事件”** ，并且您正在查看跟踪文件或表，则跟踪过程中记录的所有事件都将显示在跟踪窗口中。  
  
 **显示所有列**  
 显示所有可用数据列。 默认情况下，仅显示选定的数据列。 取消选中此框，将隐藏 **“事件选择”** 网格中所有未选定的数据列。  
  
 **列筛选器**  
 启动“编辑筛选器”对话框，该对话框将在已筛选数据列的列标签左侧显示筛选器图标。 使用 **“编辑筛选器”** 对话框可编辑数据列筛选器。  
  
 **组织列**  
 选择要跟踪的**事件**和数据列后，单击“组织列”将强制网格对跟踪结果窗口中的列重新排序。  
  
## <a name="see-also"></a>请参阅  
 [指定跟踪文件的事件和数据列&#40;SQL Server 事件探查器&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [在跟踪中筛选事件&#40;SQL Server 事件探查器&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [查看筛选器信息 (SQL Server Profiler)](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [修改筛选器&#40;SQL Server 事件探查器&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [SQL Server 事件探查器](../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Profiler 模板和权限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
  
  