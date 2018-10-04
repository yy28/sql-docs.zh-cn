---
title: 任务 2： 测试和发布匹配策略 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0e6f8fbd3ffbfcee4db212a22d4aef223450e41c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174457"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>任务 2：测试和发布匹配策略
  在此任务中，测试和发布**删除重复供应商**匹配策略。  
  
1.  在中**匹配结果**页上，单击**启动**可以测试整个策略。 对于您，此策略中只有唯一的一条规则，因此，测试此规则和策略的结果应该相同。  
  
2.  在列表框中查看所有匹配的记录及其匹配分数。 有一条记录**绿色**与之关联的图标是它之前的透视记录的副本。 示例如下：  
  
    1.  使用记录**记录 ID: 1000005**匹配的记录**记录 Id: 1000004**与**分数： 100%** 因为两个记录具有相同的值**SupplierID （先决条件）**，**供应商名称**，并**ContactEmailAddress 列**。 DQS 随机选择一条记录作为群集的透视记录。  
  
    2.  记录**1000023**记录的匹配**1000022**匹配分数： 93%，因为两个记录具有相同的值**SupplierID （先决条件）** 和**供应商名称**列，但不同的值**ContactEmailAddress**列。  
  
    3.  滚动到要查看具有记录 Id 的两个记录的列表的底部： **1000051**并**1000052**。 记录**1000052**被视为匹配分数匹配**91%** 因为两个记录具有相同的值**SupplierID**和**ContactEmailAddress**列，但不同的值**Supplier Name**列。  
  
     ![策略定义-策略结果](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "策略定义-策略结果")  
  
3.  右键单击任何匹配的记录 （具有绿色图标），然后单击**查看详细信息**若要查看有关每个字段分数对总匹配分数的贡献如匹配的更多详细信息。  
  
     ![匹配分数详细信息对话框](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "匹配分数详细信息对话框")  
  
4.  单击**关闭**以关闭**匹配分数详细信息**对话框。  
  
5.  单击**匹配结果**在页面底部的选项卡。 此选项卡向您提供了详细信息，例如匹配的记录数、不匹配的记录数、具有匹配记录的群集数、平均群集大小、最小群集大小和最大群集大小。 请参阅[创建匹配策略](http://msdn.microsoft.com/library/hh270290.aspx)的更多详细信息。 您无法从此活动中导出结果。 您刚刚使用示例数据定义了一个匹配策略，以对照示例数据测试规则和策略。  
  
     ![匹配结果选项卡](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "匹配结果选项卡")  
  
6.  单击**完成**以完成创建匹配策略。  
  
    > [!NOTE]  
    >  您已在此定义了匹配策略；因此，您无法将结果导出到输出文件。 大致说来，您使用了示例输入文件，创建了规则，并且为了定义策略而对照示例数据测试了规则和策略。  
  
7.  在 SQL Server Data Quality Services 对话框中，单击**发布**然后单击**确定**消息框上。 现在，您定义的匹配策略发布到**供应商**知识库。 您可以使用此知识库来针对输入文件运行匹配过程，以确定和解决重复项。  
  
## <a name="next-step"></a>下一步  
 [任务 3：创建并运行数据质量项目以进行匹配](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
