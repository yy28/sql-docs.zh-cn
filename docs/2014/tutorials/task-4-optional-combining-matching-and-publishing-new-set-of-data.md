---
title: 任务4（可选）：合并、匹配和发布新的数据集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13a13f03-b307-4555-8e33-6d98c459d994
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2d27a5bcd87ffd84b33de229d955dc9494846a72
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489274"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>任务 4（可选）：组合、匹配和发布新数据集
  随着时间的推移，您将会想要向 MDS 存储库中添加更多的数据。 在添加数据前，将新数据与已在 MDS 中进行管理的数据进行比较可能会很有用，以确保不会添加重复数据或不准确的数据。 在用于 Excel 的 Master Data Services 外接程序中，您可以合并两个工作表的数据并比较数据以在将数据发布到 MDS 前识别并删除重复项。 MDS Excel 外接程序的匹配功能使用 DQS 匹配功能来识别数据中的匹配项。 在本任务中，您将两个工作表中的数据合并到一个工作表中，然后执行匹配活动以在发布到 MDS 前识别并删除重复项。 有关更多详细信息，请参阅[MDS Add-in for Excel 中的数据质量匹配](https://msdn.microsoft.com/library/hh548681.aspx)和[组合数据](https://msdn.microsoft.com/library/hh548680.aspx)主题。  
  
1.  启动**Excel**的新实例。 单击 "**开始**"，指向 "**运行**"，键入**Excel**，然后单击 **"确定"**。  
  
2.  通过单击菜单栏上的 "**主数据**" 切换到 "**主数据**" 选项卡。  
  
3.  单击**连接和加载**组中的功能区上的 "**连接**" 以连接到**MDS 服务器**。 您在本课前面已配置了此连接。  
  
     ![Excel - 在“主数据”选项卡上显示“资源管理器”按钮](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel - 在“主数据”选项卡上显示“资源管理器”按钮")  
  
4.  你应看到右侧的 "**主数据资源管理器**" 窗格。 如果看不到主数据资源管理器，请单击功能区上的 "**显示资源管理器**" 按钮。  
  
5.  在 "**主数据资源管理器**" 窗口中，选择**模型**下拉列表中的 "**供应商**"。 应会看到该模型具有一个实体：**供应商**。  
  
     ![Excel -“主数据资源管理器”窗口](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel -“主数据资源管理器”窗口")  
  
6.  双击实体列表中的 "**供应商**"，将实体成员加载到 Excel 工作表中。  
  
7.  单击底部的 " **Sheet2** " 切换到 " **sheet2** " 选项卡。如果看不到**Sheet2**，请添加一个新的工作表。  
  
8.  打开 "**供应商 .xls** " 文件（包含在教程文件中的原始输入文件），并将**CombineAndCleanse**工作表中的所有（三个）行复制到**Sheet2**。  
  
9. 切换回连接到**MDS**的**Microsoft Excel** （不是**清理和匹配的供应商列表**Excel）中的**供应商**工作表。  
  
10. 单击菜单栏上的 "**主数据**"。  
  
11. 在功能区上单击 "**合并数据**"。 您将看到 "**合并数据**" 对话框。  
  
12. 在 "**合并数据**" 对话框中，单击 "**要与 MDS 数据组合的范围**" 文本框旁的按钮，如下图所示。  
  
     ![Excel -“合并数据”对话框](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel -“合并数据”对话框")  
  
13. 您现在应看到收缩的对话框。 现在，单击 " **sheet2** " 切换到 " **sheet2** " 选项卡，该选项卡具有包含4行的新供应商数据（包括一个标题行）。  
  
14. 在**Sheet2**中，选择**包括标题行的所有行**（即使它们看起来已经处于选中状态）。 应会看到**要与 MDS 数据组合的范围**自动更新。  
  
     ![Excel -“合并数据”对话框 - 最小化](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel -“合并数据”对话框 - 最小化")  
  
15. 切换回 "**供应商**" 选项卡，而不关闭 "**合并数据**" 对话框。  
  
16. 单击**文本框**旁边的**按钮**。 您现在应看到对话框已展开。 应会看到**供应商**MDS**实体**列与**Excel**列之间的所有映射都将自动填充。  
  
     ![Excel -使用数据填充的“合并数据”对话框](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel -使用数据填充的“合并数据”对话框")  
  
17. 确保将**代码**实体列映射到工作表中的 "**供应商**" 列，并将 "**邮政编码**" 实体列映射到工作表中的**邮政编码**列。  
  
18. 在 "**合并数据**" 对话框中，单击 "**合并**"。  
  
19. 确认将三个数据行添加到了工作表的底部且它们应用颜色标记出来。  
  
     ![Excel - 合并后的新元素](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel - 合并后的新元素")  
  
20. 单击功能区上的 "**数学数据**" 以标识重复项。 此功能使用 DQS 的匹配功能。  
  
21. 在 "**匹配数据**" 对话框中，选择 " **DQS 知识库**" 的 "**供应商**"。  
  
     ![Excel -“匹配数据”对话框](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel -“匹配数据”对话框")  
  
22. 将工作表列映射到域，如下表中所示。  
  
    |工作表列|Domain|  
    |----------------------|------------|  
    |Code（您上载了 Supplier ID 作为 MDS 中 Supplier 实体的代码）|Supplier ID|  
    |Name（您上载了 Supplier Name 作为 MDS 中 Supplier 实体的名称）|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. 选择 "**代码**列映射的**先决条件**"。  
  
24. 输入**70%** 作为**供应商名称**的**权重**，输入**30%** 作为**联系电子邮件****的权重**，如图所示。  
  
25. 单击" **确定**"。  
  
26. 匹配过程应为供应商标识一个重复项，**代码为： S1**。  
  
     ![Excel - 匹配结果](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel - 匹配结果")  
  
27. 选择**重复行（橙色）**，右键单击，然后单击 "**删除**" 以删除该行。  
  
28. 删除**CLUSTER_ID**列，因为不再需要它。  
  
29. 单击 "**发布**"，将具有**代码 S66**和**S57**的其他两个新记录发布到 MDS。  
  
30. 在 "**发布并**添加批注" 对话框中，添加一个**批注**，然后单击 "**发布**"。  
  
31. 切换到**主数据管理器 Web 应用程序**。  
  
32. 在主页上，确保已为**模型**选择 "**供应商**"，然后单击 "**资源管理器**"。 如果已打开**资源管理器**，请刷新 internet 浏览器。  
  
33. 按**代码****对列表进行排序**，并使用**S57**和**S66**作为代码查找记录。 您也可以使用工具栏上的 "**筛选器**" 按钮在列表中搜索特定记录。  
  
34. 现在，关闭**Book1-Microsoft Excel**窗口而不保存该文件。  
  
## <a name="next-step"></a>下一步  
 [任务 5：从 Excel 中创建基于域的属性](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
