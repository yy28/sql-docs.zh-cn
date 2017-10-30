---
title: "查看优化建议 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: e4e690c9-434f-4b01-b4de-0b905323ddd6
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 8cb1639a291bbef1dd50ada615ef5eb61c4b226f
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="lesson-1-2---viewing-tuning-recommendations"></a>课程 1-2-查看优化建议
此任务将用到 [优化工作负荷](../../tools/dta/lesson-1-1-tuning-a-workload.md)中创建的优化会话。 使用 MyScript.sql [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本优化了 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库后，[!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问将在“建议”选项卡中显示优化结果。以下任务介绍了[!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问图形用户界面 (GUI) 中的“建议”选项卡，并指导你浏览该选项卡中提供的有关优化会话结果的信息。  
  
### <a name="view-tuning-recommendations"></a>查看优化建议  
  
1.  启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问。 请参阅 [启动数据库引擎优化顾问](../../tools/dta/lesson-1-1-launching-database-engine-tuning-advisor.md)。 请确保连接到在练习[优化工作负荷](../../tools/dta/lesson-1-1-tuning-a-workload.md)中使用的同一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
2.  在“会话监视器”窗格中双击“MySession”。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问从以前的优化会话中加载会话信息并显示**建议**选项卡。请注意，因为你接受了所有优化选项默认值（其中包括选中“优化选项”选项卡上的“不分区”选项），因此，[!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问不生成任何“分区建议”。  
  
3.  在“建议”选项卡上，使用选项卡式页面底部的滚动条可以查看所有“索引建议”列。 每一行代表[!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问建议删除或创建的一个数据库对象（索引或索引视图）。 滚动到最右边的列，并单击“定义”。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问显示**SQL 脚本预览**窗口可以在其中查看[!INCLUDE[tsql](../../includes/tsql-md.md)]创建或删除该行上的数据库对象的脚本。 单击“关闭”按钮以关闭预览窗口。  
  
    如果难以找到包含链接的“定义”，则请单击以清除选项卡式页面底部的“显示现有对象”复选框，从而减少所显示的行数。 如果清除此复选框，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问将仅显示已为其生成建议的对象。 选中“显示现有对象”复选框，可以查看 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中当前存在的所有数据库对象。 使用选项卡式页面右侧的滚动条可以查看所有对象。  
  
4.  在“索引建议”窗格中右键单击网格。 在右键单击后出现的菜单中，您可以选择或取消选择建议。 您还可以使用此菜单更改网格文本的字体。  
  
5.  单击“操作”菜单中的“保存建议”，将所有建议保存到一个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本中。 将脚本命名为 **MySessionRecommendations.sql**。  
  
    在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的查询编辑器中打开 MySessionRecommendations.sql 脚本进行查看。 通过在查询编辑器中执行脚本，可将建议应用于 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库。但现在不要执行该操作。 不运行该脚本，直接在查询编辑器中将其关闭。  
  
    另外，也可以通过单击[!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问“操作”菜单上的“应用建议”选项来应用建议。但现在不要在本练习中应用这些建议。  
  
6.  如果“建议”选项卡上存在多个建议，请清除“索引建议”网格中列出数据库对象的某些行。  
  
7.  在 **“操作”** 菜单上，单击 **“评估建议”**。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问将创建一个新的优化会话，从中可以评估 MySession 原有建议的子集。  
  
8.  输入新的“会话名称”**EvaluateMySession**，然后单击工具栏中的“开始分析”按钮。 可以对新的优化会话重复步骤 2 和步骤 3 以查看其建议。  
  
## <a name="summary"></a>摘要  
你已经查看了 MySession 优化会话的“建议”选项卡的内容，并在新的 EvaluateMySession 优化会话中评估了其建议的子集。  
  
如果在运行会话之后必须更改优化选项，则可能有必要评估优化建议的子集。 例如，如果在指定会话的优化选项时要求[!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问考虑索引视图，但在生成了建议后又决定不使用索引视图。 那么，可以使用“操作”菜单上的“评估建议”选项让[!INCLUDE[ssDE](../../includes/ssde-md.md)]优化顾问在不考虑索引视图的情况下重新评估会话。 使用“评估建议”选项时，将假设将以前生成的建议应用于当前物理设计，以获得第二个优化会话的物理设计。  
  
在“报告”选项卡中可以查看更多优化结果信息，这将在本课程的下一个任务中介绍。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[查看优化报表](../../tools/dta/lesson-1-3-viewing-tuning-reports.md)  
  
  
  

