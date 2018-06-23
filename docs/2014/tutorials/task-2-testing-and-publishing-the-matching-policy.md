---
title: 任务 2： 测试和发布匹配策略 |Microsoft 文档
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8f67535e5ad4969983b06fcb710c1dfce1d97cb4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126654"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>任务 2：测试和发布匹配策略
  在此任务中，测试和发布**删除重复的供应商**匹配策略。  
  
1.  在**匹配结果**页上，单击**启动**要测试整个策略。 对于您，此策略中只有唯一的一条规则，因此，测试此规则和策略的结果应该相同。  
  
2.  在列表框中查看所有匹配的记录及其匹配分数。 已记录**绿色**与之关联的图标是它前面的透视记录的副本。 示例如下：  
  
    1.  记录**记录 ID: 1000005**的记录的匹配项**记录 Id: 1000004**与**分数： 100%** 因为这两个记录具有相同的值为**供应商 Id （先决条件）**，**供应商名称**，和**ContactEmailAddress 列**。 DQS 随机选择一条记录作为群集的透视记录。  
  
    2.  记录**1000023**记录的匹配项**1000022**与匹配分数： 93%因为两个记录都具有相同的值**供应商 Id （先决条件）** 和**供应商名称**列，但具有不同的值**ContactEmailAddress**列。  
  
    3.  滚动到列表以查看具有记录 Id 的两个记录的底部： **1000051**和**1000052**。 记录**1000052**被视为包含匹配分数的匹配项**91%** 因为两个记录都具有相同的值**供应商 Id**和**ContactEmailAddress**列，但具有不同的值**供应商名称**列。  
  
     ![策略定义的策略结果](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "策略定义的策略结果")  
  
3.  右键单击任何匹配记录 （带绿色图标），然后单击**查看详细信息**若要查看有关每个字段分数对的总匹配分数的贡献如匹配的更多详细信息。  
  
     ![匹配分数详细信息对话框](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "匹配分数详细信息对话框")  
  
4.  单击**关闭**关闭**匹配分数详细信息**对话框。  
  
5.  单击**匹配结果**在页面底部的选项卡。 此选项卡向您提供了详细信息，例如匹配的记录数、不匹配的记录数、具有匹配记录的群集数、平均群集大小、最小群集大小和最大群集大小。 请参阅[Create a Matching Policy](http://msdn.microsoft.com/library/hh270290.aspx)有关详细信息。 您无法从此活动中导出结果。 您刚刚使用示例数据定义了一个匹配策略，以对照示例数据测试规则和策略。  
  
     ![匹配结果 选项卡](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "匹配结果 选项卡")  
  
6.  单击**完成**以完成创建匹配策略。  
  
    > [!NOTE]  
    >  您已在此定义了匹配策略；因此，您无法将结果导出到输出文件。 大致说来，您使用了示例输入文件，创建了规则，并且为了定义策略而对照示例数据测试了规则和策略。  
  
7.  在 SQL Server Data Quality Services 对话框中，单击**发布**单击**确定**消息框上。 现在，你定义的匹配策略发布到**供应商**知识库。 您可以使用此知识库来针对输入文件运行匹配过程，以确定和解决重复项。  
  
## <a name="next-step"></a>下一步  
 [任务 3：创建并运行数据质量项目以进行匹配](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  