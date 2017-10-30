---
title: "创建跟踪模板 （SQL Server 事件探查器） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- saving trace template
ms.assetid: 025868b0-3790-4cda-8757-5a58327bfba0
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4834d9022ec4ea6f1b97220a38a9b84f4634dbe5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-trace-template-sql-server-profiler"></a>创建跟踪模板 (SQL Server Profiler)
  本主题介绍如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]创建新的跟踪模板。  
  
### <a name="to-create-a-trace-template"></a>创建跟踪模板  
  
1.  在 **“文件”** 菜单上，指向 **“模板”**，然后单击 **“新建模板”**。  
  
2.  在 **“跟踪模板属性”** 对话框中，从 **“选择服务器类型”**列表中选择服务器类型。  
  
3.  在“ **新模板名称** ”框中，输入模板的名称。  
  
4.  或者，单击 **“使新模板基于现有模板”**，然后从列表中选择模板。  
  
     所有事件、数据列和筛选器的初始设置都由选定模板指定。  
  
5.  或者，单击 **“用作所选服务器类型的默认模板”**。  
  
6.  在 **“事件选择”** 选项卡上，添加、删除或修改事件、数据列或筛选器。  
  
7.  在 **“事件选择”**选项卡上，使用网格控件来添加或删除跟踪文件中的事件和数据列，如下所示：  
  
    -   若要添加事件，请在 **“事件”** 列中展开相应的事件类别，再选择事件名称。  
  
    -   添加事件时，默认情况下将包含所有相关数据列。 若要从跟踪中删除某个事件的数据列，请清除此事件的该数据列中的复选框。  
  
    -   若要添加筛选器，请单击数据列的名称，然后在 **“编辑筛选器”** 对话框中指定筛选条件。 也可以右键单击数据列名称，再单击“编辑列筛选器”，以启动“编辑筛选器”对话框。 单击 **“确定”** 以添加筛选器。  
  
8.  单击“保存”。  
  
## <a name="see-also"></a>另请参阅  
 [为跟踪文件 &#40; 指定的事件和数据列SQL Server 事件探查器 &#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [从正在运行的跟踪 &#40; 派生模板SQL Server 事件探查器 &#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [从跟踪文件或跟踪表 &#40; 派生模板SQL Server 事件探查器 &#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler 模板和权限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

