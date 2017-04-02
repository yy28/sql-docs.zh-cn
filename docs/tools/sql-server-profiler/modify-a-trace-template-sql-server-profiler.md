---
title: "修改跟踪模板 (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "模板 [SQL Server], 跟踪"
  - "跟踪模板 [SQL Server]"
  - "修改跟踪"
ms.assetid: b81df2a1-e202-43d8-92b0-0beb145f0116
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 26
---
# 修改跟踪模板 (SQL Server Profiler)
  本主题介绍了如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]修改跟踪模板。  
  
### 修改跟踪模板  
  
1.  在 **“文件”** 菜单上，指向 **“模板”**，然后单击 **“编辑模板”**。  
  
2.  在 **“跟踪模板属性”** 对话框的 **“常规”** 选项卡上，可以修改服务器类型和模板名称，或者选择将默认模板用于服务器类型。  
  
3.  在“事件选择”选项卡上，使用网格控件来添加或删除跟踪文件中的事件和数据列，如下所示：  
  
    -   若要添加事件，请在 **“事件”** 列中展开相应的事件类别，再选择事件名称。  
  
    -   添加事件时，默认情况下将包含所有相关数据列。 若要从跟踪中删除某个事件的数据列，请清除此事件的该数据列中的复选框。  
  
    -   若要添加筛选器，请单击数据列的名称，然后在 **“编辑筛选器”** 对话框中指定筛选条件。 也可以右键单击数据列名称，再单击“编辑列筛选器”，以启动“编辑筛选器”对话框。 单击 **“确定”** 以添加筛选器。  
  
4.  单击“保存”，或单击“另存为”将跟踪模板另存为其他名称。  
  
## 另请参阅  
 [指定跟踪文件的事件和数据列 (SQL Server Profiler)](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [从正在运行的跟踪中派生模板 (SQL Server Profiler)](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [从跟踪文件或跟踪表派生模板 (SQL Server Profiler)](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler 模板和权限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  