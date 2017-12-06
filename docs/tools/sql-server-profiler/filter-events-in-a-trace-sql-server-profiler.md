---
title: "筛选跟踪 （SQL Server 事件探查器） 中的事件 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: 0fd63573-3b35-4f67-9e1e-ed9aabee11a8
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2111de43f590ebae4a89252b17a2ae8a40be0050
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="filter-events-in-a-trace-sql-server-profiler"></a>在跟踪中筛选事件 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]筛选器将限制跟踪内收集的事件。 如果没有设置筛选器，则跟踪输出中将返回选定事件类的所有事件。 并不一定要为跟踪设置筛选器。 但筛选器可使跟踪过程中造成的开销最小化。  
  
 可以使用 **“跟踪属性”** 或 **“跟踪模板属性”** 对话框中的 **“事件选择”** 选项卡向跟踪定义中添加筛选器。  
  
### <a name="to-filter-events-in-a-trace"></a>在跟踪中筛选事件  
  
1.  在 **“跟踪属性”** 或 **“跟踪模板属性”** 对话框中，单击 **“事件选择”** 选项卡。  
  
     **“事件选择”** 选项卡包含一个网格控件。 网格控件是包含所有可跟踪事件类的表。 每个事件类在表中占一行。 事件类可能略有不同，这取决于所连接服务器的类型和版本。 事件类由网格的“事件” **“事件”**列进行标识，并按事件类别进行分组。 其余列则列出每个事件类可以返回的数据列。  
  
2.  单击 **“列筛选器”.**  
  
     此时将显示“编辑筛选器”对话框。 **编辑筛选器**对话框中包含可用于筛选跟踪中的事件的比较运算符的列表。  
  
3.  若要应用筛选器，请单击比较运算符，再键入要用于该筛选器的值。  
  
4.  单击 **“确定”**。  
  
 **注意事项：**  
  
-   如果要对“事件选择”选项卡上的 **StartTime** 和 **EndTime** 数据列设置筛选条件，那么请确保：  
  
    -   输入的日期符合此格式： `YYYY/MM/DD HH:mm:sec`。  
  
         -或者-  
  
    -   在**“常规选项”** 对话框中选中了 **“使用区域设置来显示日期和时间值”** 。 若要查看**常规选项**对话框中，在[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]**工具**菜单上，单击**选项**。  
  
         -以及-  
  
    -   输入的日期介于 1753 年 1 月 1 日到 9999 年 12 月 31 日之间。  
  
-   如果从 **osql** 实用工具或 **sqlcmd** 实用工具跟踪事件，则始终将 **%** 追加到 **TextData** 数据列上的筛选器。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
