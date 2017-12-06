---
title: "优化工作负荷 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords: workloads [SQL Server], tuning
ms.assetid: 6229bf3f-1182-4bc6-8451-cedc37f4b62e
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 56041b15a6fa78bc88d62c409f0df958d0dd862a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-1-1---tuning-a-workload"></a>课程 1-1-优化工作负荷
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]数据库引擎优化顾问可以用于查找的数据库和你选择进行优化的表的查询性能的最佳物理数据库设计。  
  
此任务使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库。 为了增强安全性，默认情况下不会安装示例数据库。 若要安装示例数据库，请参阅 [安装 SQL Server 示例和示例数据库](http://sqlserversamples.codeplex.com)。  
  
### <a name="tune-a-workload-transact-sql-script-file"></a>优化工作负荷 Transact-SQL 脚本文件  
  
1.  从  [SELECT 示例 (Transact-SQL)](../../t-sql/queries/select-examples-transact-sql.md) 中的“A. 使用 SELECT 检索行和列”复制示例 SELECT 语句或语句，并将语句粘贴到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的查询编辑器中。 将该文件保存为**MyScript.sql**，并存储在可以轻松找到的目录中。  
  
2.  启动数据库引擎优化顾问。 请参阅[启动数据库引擎优化顾问](../../tools/dta/lesson-1-1-launching-database-engine-tuning-advisor.md)。  
  
3.  在数据库引擎优化顾问 GUI 右窗格的“会话名称”中，键入 **MySession**。  
  
4.  针对“工作负荷”选择“文件”，再单击“查找工作负荷文件”按钮，以查找在步骤 1 中保存的 **MyScript.sql** 文件。  
  
5.  在“用于工作负荷分析的数据库”列表中选择 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，或在“选择要优化的数据库和表”网格中选择 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，使“保存优化日志”保持选中状态。 “用于工作负荷分析的数据库”指定数据库引擎优化顾问在优化工作负荷时连接到的第一个数据库。 优化开始之后，数据库引擎优化顾问连接到由工作负荷中包含的 `USE DATABASE` 语句所指定的数据库。  
  
6.  单击“优化选项”选项卡。不必为本练习设置任何优化选项，但请花些时间来查看默认的优化选项。 按 F1 键可查看该选项卡式页面的帮助。 单击“高级选项”可查看其他的优化选项。 请在“高级优化选项”对话框中单击“帮助”，以了解有关此处所显示的优化选项的信息。 单击“取消”关闭“高级优化选项”对话框，并保留选中默认选项。  
  
7.  在工具栏中，单击 **“开始分析”** 按钮。 在数据库引擎优化顾问分析工作负荷时，可以监视“进度”选项卡上的状态。优化完成后，“建议”选项卡随即显示。  
  
    如果收到有关优化结束日期和时间的错误，请检查主“优化选项”选项卡上的“结束时间”。请确保“结束时间”的日期和时间晚于当前的日期和时间，必要时可进行更改。  
  
8.  分析完成之后，在“操作”菜单中，单击“保存建议”，将建议保存为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。 在“另存为”对话框中，导航到要保存建议脚本的目录，然后键入文件名 **MyRecommendations**。  
  
## <a name="summary"></a>摘要  
您已完成对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的简单 SELECT 语句工作负荷的优化。 数据库引擎优化顾问还可将 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 跟踪文件和表作为优化工作负荷。 下一个任务将向您展示如何查看和解释进行优化后所收到的优化建议。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[查看优化建议](../../tools/dta/lesson-1-2-viewing-tuning-recommendations.md)  
  
  
  
