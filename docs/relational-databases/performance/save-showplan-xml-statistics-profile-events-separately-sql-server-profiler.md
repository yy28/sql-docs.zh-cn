---
title: "单独保存 Showplan XML Statistics Profile 事件 (SQL Server Profiler) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: df393f13-d538-4d94-8155-9c2fdf5f755d
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1f079c68f7f54569dee1a6d9f2e9fa61f1893426
ms.lasthandoff: 04/11/2017

---
# <a name="save-showplan-xml-statistics-profile-events-separately-sql-server-profiler"></a>分别保存 Showplan XML Statistics Profile 事件 (SQL Server Profiler)
  本主题说明如何使用 **将在跟踪中捕获的** Showplan XML Statistics Profile [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]事件保存到单独的 .SQLPlan 文件中。 可以在 **中打开** Showplan XML Statistics Profile [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]事件文件，这样您就可以查看每个事件的图形执行计划。  
  
### <a name="to-save-showplan-xml-statistics-events-separately"></a>分别保存 Showplan XML Statistics 事件  
  
1.  在 **“文件”** 菜单上，单击 **“新建跟踪”**，再连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。  
  
     此时，将显示 **“跟踪属性”** 对话框。  
  
    > [!NOTE]  
    >  如果你选中了“建立连接后立即开始跟踪”****，那么系统不会显示“跟踪属性”****对话框，而是会开始进行跟踪。 若要关闭此设置，请在“工具”****菜单上，单击“选项”****，然后清除“建立连接后立即开始跟踪”****复选框。  
  
2.  在 **“跟踪属性”** 对话框内的 **“跟踪名称”** 框中键入跟踪的名称。  
  
3.  在 **“使用模板”** 列表中，选择要作为跟踪基础的跟踪模板，或选择 **“空”** （如果不想使用模板）。  
  
4.  执行以下操作之一：  
  
    -   单击“保存到文件”****，将跟踪内容捕获到文件中。 指定 **“设置最大文件大小”**的值。  
  
         也可以选择 **“启用文件滚动更新”** 和 **“服务器处理跟踪数据”**。  
  
    -   单击“保存到表”****，将跟踪捕获到数据库表中。  
  
         或者，单击 **“设置最大行数”**，并指定值。  
  
5.  也可以选中 **“启用跟踪停止时间”** 复选框，并指定停止的日期和时间。  
  
6.  单击“事件选择”****选项卡。  
  
7.  在“事件”****数据列中，展开“性能”****事件类别，然后选中“Showplan XML Statistics Profile”****复选框。 如果 **Performance** 事件类别不可用，请选中 **“显示所有事件”** 以显示该类别。  
  
     “事件提取设置”****选项卡将添加到“跟踪属性”****对话框中。  
  
8.  在“事件提取设置”****选项卡上，单击“分别保存 XML 显示计划事件”****。  
  
9. 在 **“另存为”** 对话框中，输入存储 **Showplan XML Statistics Profile** 事件的文件名。  
  
10. 单击“单个文件中的所有批”****，将所有“Showplan XML Statistics Profile”****事件都保存到一个 XML 文件中；或者，单击“不同文件中的每个 XML 显示计划批”****，为每个“Showplan XML Statistics Profile”****事件都新建一个 XML 文件。  
  
11. 若要在 SQL Server Management Studio 中查看 **Showplan XML Statistics Profile** 事件文件，请在 **“文件”** 菜单上，指向 **“打开”**，然后单击 **“文件”**。 导航到保存 **Showplan XML Statistics Profile** 事件文件的目录，以选择一个事件文件并将其打开。 **Showplan XML Statistics Profile** 事件文件的文件扩展名为 .SQLPlan。  
  
## <a name="see-also"></a>另请参阅  
 [在 SQL Server Profiler 中使用 SHOWPLAN 结果来分析查询](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  
