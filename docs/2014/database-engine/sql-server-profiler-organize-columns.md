---
title: SQL Server Profiler-组织列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.organize.columns.f1
ms.assetid: bf5674f4-da5e-43f9-aeb2-76ca37993790
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f0ad3d1204e8c27d91ecb3b586d56a27d45eeb4e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089758"
---
# <a name="sql-server-profiler---organize-columns"></a>SQL Server Profiler - 组织列
  使用 **“组织列”** 对话框可为跟踪中所显示的分组或聚合事件选择数据列，以便查看和分析较大的跟踪文件或跟踪表。  
  
 通过聚合，可以在跟踪中移动和折叠其相应的事件类类型下的所有事件。 事件类名称的左侧将显示一个加号 (**+**)。 单击加号可展开相应的事件类，以便查看该类型的所有事件。  
  
 通过分组，可以在跟踪显示窗口中将特定类型的所有事件组织起来。 但是，这些事件在其事件类类型下并不折叠显示。  
  
 在跟踪显示窗口中对事件进行分组或聚合时，所选择的用于分组或聚合的列会在显示窗口中保持固定，但是您可以左右滚动，以便查看所有其他的数据列。  
  
 若要访问此对话框，请打开现有的跟踪文件或跟踪表，再单击[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]“文件”菜单上的“属性”。 在 **“跟踪属性”** 对话框中，单击 **“事件选择”** 选项卡，再单击 **“组织列”**。 您也可以在创建新的跟踪时单击 **“事件选择”** 选项卡上的 **“组织列”** 。  
  
## <a name="options"></a>选项  
 **组**  
 将数据列名称移动到“组”下，可以在跟踪窗口中对事件类进行分组或聚合。  
  
 若要对事件进行聚合，请将一个数据列移动到 **“组”** 中。 这会导致在跟踪显示窗口中相应的事件类类型名称下折叠所有特定类型的事件。 事件类名称的左侧将显示一个加号 (**+**)。 单击加号可展开相应的事件类类型，以便查看所有事件。 您可以通过单击 **“视图”** 菜单上的 **“聚合视图”** 或 **“分组视图”** 来启用或禁用聚合和分组功能。  
  
 若要对事件进行分组，请将多个数据列移动到 **“组”** 中。 这会将跟踪显示窗口中所有特定类型的事件分到一组中，但是不会在各事件类类型名称下折叠事件。 您可以通过单击“视图”菜单上的 **“分组视图”** 在分组视图和未分组视图之间来回切换。 当多个数据列移动到 **“组”** 中时，将无法切换到 **“聚合视图”** 。  
  
 **“列”**  
 列出可移动到“组”中的数据列。 单击“列”左侧的加号 (**+**) 可展开列表。  
  
 **向上**  
 选择数据列之后，单击“向上”可将数据列移动到“组”中。 您也可以单击 **“向上”** 在跟踪显示窗口中对列的显示顺序重新进行排列。  
  
 **向下**  
 选择数据列之后，单击“向下”可将数据列从“组”中移出。 您也可以单击 **“向下”** 在跟踪显示窗口中对列的显示顺序重新进行排列。  
  
## <a name="see-also"></a>请参阅  
 [组织跟踪中显示的列&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [创建跟踪 (SQL Server Profiler)](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [创建跟踪模板 (SQL Server Profiler)](../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)   
 [打开跟踪文件 (SQL Server Profiler)](../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [打开跟踪表 (SQL Server Profiler)](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
  
