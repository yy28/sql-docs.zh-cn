---
title: 任务 4 （可选）： 组合、 匹配和发布新的数据集 |Microsoft 文档
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
ms.assetid: 13a13f03-b307-4555-8e33-6d98c459d994
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4ab096c1f43fbeab2165e1e32a83f2ba854b3b13
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026037"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>任务 4（可选）：组合、匹配和发布新数据集
  随着时间的推移，您将会想要向 MDS 存储库中添加更多的数据。 在添加数据前，它可用于对已在 MDS，以确保不添加重复或不准确的数据中管理数据的新数据进行比较。 在用于 Excel 的 Master Data Services 外接程序中，您可以合并两个工作表的数据并比较数据以在将数据发布到 MDS 前识别并删除重复项。 MDS Excel 外接程序的匹配功能使用 DQS 匹配功能来识别数据中的匹配项。 在本任务中，您将两个工作表中的数据合并到一个工作表中，然后执行匹配活动以在发布到 MDS 前识别并删除重复项。 请参阅[MDS add-in for Excel 中的数据质量匹配](http://msdn.microsoft.com/library/hh548681.aspx)和[合并数据](http://msdn.microsoft.com/library/hh548680.aspx)更多详细信息的主题。  
  
1.  启动新实例**Excel**。 单击**启动**，指向**运行**，类型**Excel**，然后单击**确定**。  
  
2.  切换到**主数据**选项卡上通过单击**主数据**菜单栏上。  
  
3.  单击**连接**在功能区中**连接并加载**组连接到**MDS 服务器**。 您在本课前面已配置了此连接。  
  
     ![Excel-在主数据 Tabl 显示资源管理器按钮](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel-在主数据 Tabl 显示资源管理器按钮")  
  
4.  你应该会看到**主数据资源管理器**右侧的窗格。 如果看不到主数据资源管理器，请单击**显示资源管理器**功能区上的按钮。  
  
5.  在**主数据资源管理器**窗口中，选择**供应商**的下拉列表中**模型**。 你应该会看到该模型具有一个实体：**供应商**。  
  
     ![Excel-主数据资源管理器窗口](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel 的主数据资源管理器窗口")  
  
6.  双击**供应商**要加载到 Excel 工作表的实体成员的实体列表中。  
  
7.  单击**Sheet2**底部以切换到**Sheet2**选项卡。如果看不到**Sheet2**，添加一个新工作表。  
  
8.  打开**Suppliers.xls**文件 （的原始输入的文件包含在教程的文件），并将从所有 （三个） 的行复制**CombineAndCleanse**工作表**Sheet2**。  
  
9. 切换回**供应商**工作表中**Book 1 – Microsoft Excel** (不**Cleansed 和匹配供应商列表**Excel) 的已连接到**MDS**.  
  
10. 单击**主数据**菜单栏上。  
  
11. 单击**合并数据**功能区上。 你将看到**合并数据**对话框。  
  
12. 在**合并数据**对话框框中，单击下一步按钮**要与 MDS 数据组合范围**文本框中，如下图中所示。  
  
     ![Excel-合并数据对话框](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel-合并数据对话框")  
  
13. 您现在应看到收缩的对话框。 现在，单击**Sheet2**切换到**Sheet2**具有 4 行 （包括一个标题行） 与新的供应商数据的选项卡。  
  
14. 在**Sheet2**，选择**包括标头行的所有行**（即使它们看起来处于已选中状态）。 你应该会看到**要与 MDS 数据组合范围**自动更新。  
  
     ![Excel-合并数据对话框中的最小化](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel-合并数据的最小化对话框")  
  
15. 切换回**供应商**无需关闭的选项卡**合并数据**对话框。  
  
16. 单击**按钮**旁边**文本框**。 您现在应看到对话框已展开。 你应看到的各个栏之间的所有映射**供应商**MDS**实体**到**Excel**将自动填充列。  
  
     ![Excel-合并数据对话框中，用数据填充](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel-合并数据对话框中，用数据填充")  
  
17. 确保**代码**实体列映射到**供应商 Id**工作表中的列和**邮政编码**实体列映射到**邮政编码**工作表中的列。  
  
18. 上**合并数据**对话框中，单击**组合**。  
  
19. 确认将三个数据行添加到了工作表的底部且它们应用颜色标记出来。  
  
     ![Excel-组合后的新元素](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel-组合后的新元素")  
  
20. 单击**数学数据**来标识重复在功能区上。 此功能使用 DQS 的匹配功能。  
  
21. 在**匹配数据**对话框中，选择**供应商**为**DQS 知识库**。  
  
     ![Excel-匹配数据对话框](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel-匹配数据对话框")  
  
22. 将工作表列映射到域，如下表中所示。  
  
    |工作表列|域|  
    |----------------------|------------|  
    |Code（您上载了 Supplier ID 作为 MDS 中 Supplier 实体的代码）|Supplier ID|  
    |Name（您上载了 Supplier Name 作为 MDS 中 Supplier 实体的名称）|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. 选择**先决条件**为**代码**列映射。  
  
24. 输入**70%** 作为**权重**为**供应商名称**和**30%** 作为**权重**为**联系人电子邮件**图中所示。  
  
25. 单击“确定” 。  
  
26. 匹配过程应与供应商标识一个重复**代码： S1**。  
  
     ![Excel-匹配结果](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel-匹配的结果")  
  
27. 选择**重复行 （橙色）**，右键单击，然后单击**删除**删除该行。  
  
28. 删除**CLUSTER_ID**列，因为你不再需要它。  
  
29. 单击**发布**发布的其他两个新记录与**代码 S66**和**S57**到 MDS。  
  
30. 在**发布并添加批注**对话框框中，添加**批注**，然后单击**发布**。  
  
31. 切换到**主数据管理器 Web 应用程序**。  
  
32. 在主页上，确保**供应商**为选择**模型**，然后单击**资源管理器**。 如果你已有**资源管理器**打开，请刷新 internet 浏览器。  
  
33. **排序**列表**代码**和查找的记录与**S57**和**S66**作为代码。 你还可以使用**筛选器**搜索列表中的特定记录工具栏上的按钮。  
  
34. 现在，关闭**Book1 – Microsoft Excel**窗口而不保存该文件。  
  
## <a name="next-step"></a>下一步  
 [任务 5：从 Excel 中创建基于域的属性](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  