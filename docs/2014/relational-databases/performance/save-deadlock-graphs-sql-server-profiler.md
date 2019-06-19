---
title: 保存死锁图形 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], saving deadlock graphs
- graphs [SQL Server]
- saving deadlock graphs
ms.assetid: bf1fc906-abd6-4a89-842e-da0d66b2defe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 33757ad1f8085ce141b8e206f2c3fd99c7dcba90
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150706"
---
# <a name="save-deadlock-graphs-sql-server-profiler"></a>保存死锁图形（SQL Server 事件探查器）
  本主题介绍了如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]保存 Deadlock Graph 事件。 Deadlock Graph 事件以 XML 文件形式保存。  
  
### <a name="to-save-deadlock-graph-events-separately"></a>分别保存 Deadlock Graph 事件  
  
1.  在 **“文件”** 菜单上，单击 **“新建跟踪”** ，再连接到 SQL Server 实例。  
  
     将出现“跟踪属性”对话框。 **“跟踪属性”** 对话框。  
  
    > [!NOTE]  
    >  如果选择“建立连接后立即开始跟踪”  ，则不会显示“跟踪属性”  对话框，而是开始跟踪。 若要关闭此设置，请在“工具”  菜单上，单击“选项”  ，然后清除“建立连接后立即开始跟踪”  复选框。  
  
2.  在“跟踪属性”对话框内的“跟踪名称”  框中键入跟踪的名称。  
  
3.  在 **“使用模板”** 列表中，为此跟踪选择一个跟踪模板；如果不想使用模板，请选择 **“空白”** 。  
  
4.  执行以下操作之一：  
  
    -   选中“保存到文件”  复选框以将跟踪捕获到文件中。 指定 **“设置最大文件大小”** 的值。  
  
         也可以选择 **“启用文件滚动更新”** 和 **“服务器处理跟踪数据”** 。  
  
    -   选中 **“保存到表”** 复选框以将跟踪捕获到数据库表中。  
  
         根据需要，可以单击 **“设置最大行数”** ，并指定值。  
  
5.  根据需要，可以选中 **“启用跟踪停止时间”** 复选框，再指定停止日期和时间。  
  
6.  单击“事件选择”  选项卡。  
  
7.  在“事件”  数据列中，展开“Locks”  事件类别，然后选中“Deadlock Graph”  复选框。 如果没有显示“Locks”事件类别，请选中 **“显示所有事件”** 以显示该类别。  
  
     “事件提取设置”  选项卡将添加到“跟踪属性”  对话框中。  
  
8.  在“事件提取设置”  选项卡上，单击“分别保存死锁 XML 事件”  。  
  
9. 在 **“另存为”** 对话框中，输入要存储 Deadlock Graph 事件的文件的名称。  
  
10. 单击“单个文件中的所有死锁 XML 批”  以将所有 Deadlock Graph 事件保存到单个 XML 文件中，或单击“不同文件中的每个死锁 XML 批”  以便为每个 Deadlock Graph 事件创建新的 XML 文件。  
  
 保存死锁文件后，您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中打开该文件。 有关详细信息，请参阅[如何打开、查看和打印死锁文件 (SQL Server Management Studio)](open-view-and-print-a-deadlock-file-sql-server-management-studio.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用 SQL Server Profiler 分析死锁](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)  
  
  
