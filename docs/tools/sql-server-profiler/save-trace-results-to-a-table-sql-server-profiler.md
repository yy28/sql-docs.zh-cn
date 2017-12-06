---
title: "将跟踪结果保存到表 （SQL Server 事件探查器） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- saving traces
- traces [SQL Server], saving
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 47c21a4e8505dedbb6f9b811aba09302aeaf019b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>将跟踪结果保存到表 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]本主题介绍如何将跟踪结果保存到数据库表中，通过使用[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。  
  
### <a name="to-save-trace-results-to-a-table"></a>将跟踪结果保存到表  
  
1.  在 **“文件”** 菜单上，单击 **“新建跟踪”**，再连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。  
  
     将出现“跟踪属性”对话框。 **“跟踪属性”**对话框。  
  
    > [!NOTE]  
    >  如果选择“建立连接后立即开始跟踪”，则不会显示“跟踪属性”对话框，而是开始跟踪。 若要关闭此设置，请在“工具”菜单上，单击“选项”，然后清除“建立连接后立即开始跟踪”复选框。  
  
2.  在 **“跟踪名称”** 框中，键入跟踪的名称，然后单击 **“保存到表”**。  
  
3.  在 **“连接到服务器”** 对话框中，连接到将包含跟踪表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。  
  
4.  在“目标表”对话框中，从“数据库”列表中选择一个数据库。  
  
5.  在 **“所有者”** 列表中，选择此跟踪的所有者。  
  
6.  在 **“表”** 列表中，键入或选择跟踪结果的表名。 单击“确定” **。**  
  
7.  在“跟踪属性”对话框中，选中“设置最大行数(以千为单位)”复选框以指定要保存的最大行数。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
