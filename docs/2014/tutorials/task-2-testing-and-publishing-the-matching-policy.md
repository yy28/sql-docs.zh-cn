---
title: 任务2：测试和发布匹配策略 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a9957625e09bde8bb733eca6e564dfdcfbb0bd98
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484731"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>任务 2：测试和发布匹配策略
  在此任务中，您将测试并发布**删除重复的供应商**匹配策略。  
  
1.  在 "**匹配结果**" 页上，单击 "**启动**" 以测试整个策略。 对于您，此策略中只有唯一的一条规则，因此，测试此规则和策略的结果应该相同。  
  
2.  在列表框中查看所有匹配的记录及其匹配分数。 具有与之关联的**绿色**图标的记录是其前面的透视记录的副本。 示例如下：  
  
    1.  记录 ID 为**1000005**的记录与**记录 id： 1000004**的记录匹配，**分数为： 100%** ，因为这两条记录对于**供应商（必备）**、**供应商名称**和**ContactEmailAddress 列**都具有相同的值。 DQS 随机选择一条记录作为群集的透视记录。  
  
    2.  记录**1000023**是匹配分数为的记录**1000022**的匹配项：93%，因为这两条记录对**供应商****姓名**列具有相同的值，但**ContactEmailAddress**列的值不同。  
  
    3.  滚动到列表底部，查看记录 Id 为**1000051**和**1000052**的两个记录。 记录**1000052**被视为匹配分数为**91%** 的匹配，因为这两条记录对供应**商**和**ContactEmailAddress**列具有相同的值，但**供应商名称**列的值不同。  
  
     ![策略定义 - 策略结果](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "策略定义 - 策略结果")  
  
3.  右键单击任何匹配的记录（带有绿色图标），然后单击 "**查看详细信息**" 以查看有关匹配项的详细信息，例如每个字段分数对总体匹配分数的贡献。  
  
     ![“匹配分数详细信息”对话框](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "“匹配分数详细信息”对话框")  
  
4.  单击 "**关闭**" 以关闭 "**匹配分数详细信息**" 对话框。  
  
5.  单击页面底部的 "**匹配结果**" 选项卡。 此选项卡向您提供了详细信息，例如匹配的记录数、不匹配的记录数、具有匹配记录的群集数、平均群集大小、最小群集大小和最大群集大小。 有关更多详细信息，请参阅[创建匹配策略](https://msdn.microsoft.com/library/hh270290.aspx)。 您无法从此活动中导出结果。 您刚刚使用示例数据定义了一个匹配策略，以对照示例数据测试规则和策略。  
  
     ![“匹配结果”选项卡](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "“匹配结果”选项卡")  
  
6.  单击 "**完成**" 以完成创建匹配策略。  
  
    > [!NOTE]  
    >  您已在此定义了匹配策略；因此，您无法将结果导出到输出文件。 大致说来，您使用了示例输入文件，创建了规则，并且为了定义策略而对照示例数据测试了规则和策略。  
  
7.  在 "SQL Server Data Quality Services" 对话框中，单击 "**发布**"，然后在消息框中单击 **"确定"** 。 现在，您定义的匹配策略发布到**供应商**知识库中。 您可以使用此知识库来针对输入文件运行匹配过程，以确定和解决重复项。  
  
## <a name="next-step"></a>下一步  
 [任务 3：创建并运行数据质量项目以进行匹配](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
