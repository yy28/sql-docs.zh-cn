---
title: "在跟踪 （SQL Server 事件探查器） 中筛选服务器进程 Id (Spid) |Microsoft 文档"
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
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a41b9ade1c1336d8e2591e136054f6fd81c57eea
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>在跟踪中筛选服务器进程 ID (SPID) (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]本主题介绍如何通过使用筛选器跟踪中的服务器进程标识符 (Spid) [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。  
  
### <a name="to-filter-system-ids-in-a-trace"></a>在跟踪中筛选系统 ID  
  
1.  在 **“文件”** 菜单上，单击 **“新建跟踪”**，再连接到 SQL Server 实例。  
  
     将出现“跟踪属性”对话框。 **“跟踪属性”**对话框。  
  
    > [!NOTE]  
    >  如果选择“建立连接后立即开始跟踪”，则不会显示“跟踪属性”对话框，而是开始跟踪。 若要关闭此设置，请在“工具”菜单上，单击“选项”，然后清除“建立连接后立即开始跟踪”复选框。  
  
2.  在 **“跟踪名称”** 框中，键入跟踪的名称。  
  
3.  在“使用模板”名称列表中，选择跟踪模板。  
  
4.  根据需要，指定保存跟踪结果的目标文件或表。  
  
5.  在“事件选择”选项卡上，单击“SPID”列标题以启动“编辑筛选器”对话框。 还可以右键单击列标题，然后选择“编辑列筛选器”。 如果 **SPID** 列不出现，请选中 **“显示所有列”** 框。  
  
6.  在 **“编辑筛选器”** 对话框中，展开相应的比较运算符，输入 SPID 作为比较的值。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
