---
title: 任务 12： 发现知识 （知识发现） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dd80a8e6-1e41-4c49-9898-02b1d2505a10
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b608a384e5281134ae951fdfeca0e89234c4a32a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028253"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>任务 12：发现知识（知识发现）
  在此任务中，你将要执行**知识发现**上的活动**供应商 ID**和**供应商名称**域。 在此方案中，知识发现过程主要导入这两个域的值。  
  
 在本教程中，您是从头开始构建知识库的。 还可以通过执行知识发现活动来创建知识库。 当你单击**创建知识库**主页上，在 DQS 客户端将你带到页且**域管理**选择活动的活动。 你可以更改**活动**到**知识发现**，然后在下一页上你可以创建域知识发现过程的一部分。 请参阅[执行知识发现](http://msdn.microsoft.com/library/hh510398.aspx)有关详细信息。  
  
1.  在主页面中的 DQS 客户端中**最近的知识库**部分中，单击**右箭头**旁边**供应商**知识库和单击**知识发现**。 或者，你可以单击**打开知识库**，选择**供应商**从**知识库列表**，选择**知识发现**作为**活动**单击**下一步**。  
  
     ![在主菜单中的知识发现页](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "在主菜单中的知识发现页")  
  
2.  选择**Excel 文件**为**数据源**。  
  
3.  单击**浏览**、 导航和选择**Suppliers.xls**，然后单击**打开**。  
  
4.  选择**供应商的发现**为**工作表**。  
  
5.  在**映射**部分中，映射**供应商 Id**列从**Excel**文件为**供应商 ID**域和**供应商名称**列**供应商名称**域使用**下拉列表**。 Excel 文件包含有关的示例数据**供应商 ID**和**供应商名称**域。 在发现过程中，您可以选择要为其发现值的域。 您可以在此页上创建域，然后将源列映射到这些域。 在知识发现活动中创建域的情况并不少见，而不是在域管理活动期间创建域。  
  
     ![映射的发现过程的页](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "映射的发现过程的页")  
  
6.  单击**下一步**切换到**发现**页。  
  
7.  上**发现**页上，单击**启动**启动发现过程。 对列执行发现**供应商 Id**和**供应商名称**中**Suppliers.xls**文件。 **供应商 ID**和**供应商名称**应使用从发现获取的知识填充域。  
  
     ![发现的发现过程的页](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "发现的发现过程的页")  
  
8.  在分析完成后，请查看**来源统计信息**中**探查器选项卡**位于页的底部。 请注意，使用 10 个新记录的总 20 个值 (**供应商 Id**和**供应商名称**值从**Excel 工作表**) 中发现。 我们还看到多少个值是新的、唯一的、新并且是唯一的以及有效的。 在右侧的列表框中，您可以看到发现过程中涉及的每个域的详细信息。 如果您将鼠标悬停在“完整性”列的状态栏上，您可以看到源列中是否有任何缺失值。  
  
     ![知识发现结果](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "知识发现结果")  
  
9. 单击**下一步**切换到**管理域值**页。  
  
10. 在**管理域值**页上，单击**供应商名称**的域中的域列表。  
  
11. 在右窗格中，右键单击**延迟国家/地区 Storex** （注意 x 结尾），然后选择**Lazy 国家/地区存储**。 DQS 建议在对域运行拼写检查程序后进行此更改。 默认情况下，在您创建的域上启用拼写检查程序。  
  
     ![更正延迟国家/地区存储的供应商名称-](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "更正供应商名称-迟缓国家/地区存储")  
  
12. 在域值列表中，确认值**延迟国家/地区 Storex**被设置为错误 (红色**X**标记) 与**Lazy 国家/地区存储**为更正，还可以**Lazy 国家/地区存储**还添加为有效的值。  
  
     ![域值并为值更正](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "域值并更正为值")  
  
13. 单击 **“完成”**。  
  
14. 上**SQL Server Data Quality Services**对话框中，单击**发布**。  
  
15. 单击**确定**成功消息框上。  
  
     您已经完成本教程的第一个课程。  
  
## <a name="next-step"></a>下一步  
 [第 2 课：使用 Suppliers 知识库清理供应商数据](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  