---
title: 单独保存 Showplan XML 事件 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: 33320a7a-36e8-401c-876d-5b82c49abd85
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c92c08349a473aa4a83205cc539eec3577619109
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754189"
---
# <a name="save-showplan-xml-events-separately-sql-server-profiler"></a>分别保存 Showplan XML 事件 (SQL Server Profiler)
  本主题介绍了如何使用 **将在跟踪中捕获到的** Showplan XML [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]事件分别保存到单独的 .SQLPlan 文件中。 您可以在 **中打开** Showplan XML [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]事件文件，从中可以查看每个事件的以图形表示的执行计划。  
  
### <a name="to-save-showplan-xml-events-separately"></a>分别保存 Showplan XML 事件  
  
1.  在 **“文件”** 菜单上，单击 **“新建跟踪”**，再连接到 SQL Server 实例。  
  
     将出现“跟踪属性”对话框。 **“跟踪属性”** 对话框。  
  
    > [!NOTE]  
    >  如果选择“建立连接后立即开始跟踪”，则不会显示“跟踪属性”对话框，而是开始跟踪。 若要关闭此设置，请在“工具”菜单上，单击“选项”，然后清除“建立连接后立即开始跟踪”复选框。  
  
2.  在 **“跟踪属性”** 对话框内的 **“跟踪名称”** 框中键入跟踪的名称。  
  
3.  在 **“使用模板”** 列表中，为此跟踪选择一个跟踪模板；如果不想使用模板，请选择 **“空白”** 。  
  
4.  执行以下操作之一：  
  
    -   选中“保存到文件”复选框以将跟踪捕获到文件中。 指定 **“设置最大文件大小”** 的值。 也可以选中 **“启用文件滚动更新”** 复选框和 **“服务器处理跟踪数据”** 复选框。  
  
    -   选中“保存到表”复选框以将跟踪捕获到数据库表中。 或者，单击 **“设置最大行数”**，并指定值。  
  
5.  根据需要，可以选中 **“启用跟踪停止时间”** 复选框，再指定停止日期和时间。  
  
6.  单击“事件选择”选项卡。  
  
7.  在“事件”数据列中，展开“性能”事件类别，然后选中“Showplan XML”复选框。 如果 **Performance** 事件类别不可用，请选中 **“显示所有事件”** 以显示该类别。  
  
     “事件提取设置”选项卡将添加到“跟踪属性”对话框中。  
  
8.  在“事件提取设置”选项卡上，单击“分别保存 XML 显示计划事件”。  
  
9. 在 **“另存为”** 对话框中，输入要在其中存储 **Showplan XML** 事件的文件的名称。  
  
10. 单击“单个文件中的所有 XML 显示计划批”将所有 **Showplan XML** 事件保存到一个 XML 文件中，或单击“不同文件中的每个 XML 显示计划批”为每个 **Showplan XML** 事件创建一个新的 XML 文件。  
  
11. 若要在 SQL Server Management Studio 中查看 **Showplan XML** 事件文件，请在 **“文件”** 菜单上指向 **“打开”**，然后单击 **“文件”**。 导航到保存 **Showplan XML** 事件文件的目录，选择一个文件并打开它。 **Showplan XML** 事件文件带有 .SQLPlan 文件扩展名。  
  
## <a name="see-also"></a>请参阅  
 [在 SQL Server Profiler 中使用 SHOWPLAN 结果来分析查询](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  
