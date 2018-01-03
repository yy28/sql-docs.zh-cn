---
title: "修改筛选器 （SQL Server 事件探查器） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], modifying
- modifying filters, modifying
- filters [SQL Server], traces
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7d8d48e66b041d09dbcbbe47ec7702656e250bdf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="modify-a-filter-sql-server-profiler"></a>修改筛选器 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]向跟踪模板，其中包含跟踪定义，以限制跟踪所收集的事件数添加筛选器。 限制收集的事件数能够减少跟踪对性能的影响。 如果已设置了跟踪模板的筛选器，并发现该跟踪没有收集所需类型的信息，则可以对该筛选器进行编辑。  
  
### <a name="to-modify-a-filter"></a>修改筛选器  
  
1.  在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]中，打开要修改的跟踪筛选器的模板。 在 **“文件”** 菜单上，单击 **“模板”**，然后选择 **“编辑模板”**。  
  
2.  在 **“跟踪模板属性”** 对话框的 **“常规”** 选项卡中，选择 **“选择模板名称”** 列表中的一个模板。  
  
3.  单击 **“事件选择”** 选项卡。  
  
     **“事件选择”** 选项卡包含一个网格控件。 网格控件是包含所有可跟踪事件类的表。 每个事件类在表中占一行。 事件类可能略有不同，这取决于所连接服务器的类型和版本。 事件类由网格的“事件” **“事件”**列进行标识，并按事件类别进行分组。 其余列则列出每个事件类可以返回的数据列。  
  
4.  单击 **“列筛选器”**。  
  
5.  在 **“编辑筛选器”** 对话框中，单击要编辑的比较运算符旁边的值，然后键入新值或删除一个值。 此外，还可以添加其他筛选器。  
  
6.  单击 **“确定”** 保存模板。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
