---
title: 任务 1： 定义匹配策略 |Microsoft 文档
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
ms.assetid: 6f89a720-fce5-4f60-bef3-a159bbc9f25c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0b0ccf6217899b5368cf27f93951e0a7ddc0cf48
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026910"
---
# <a name="task-1-defining-a-matching-policy"></a>任务 1：定义匹配策略
  在本任务中，您将创建含有一个规则的匹配策略。 规则将具有一个必备项：**供应商 ID**，这意味着两个供应商 Id 必须匹配之前使用规则中的其他域。 此规则使用两个其他域：**供应商名称**与**相似性**值设置为**70%** 和**联系人电子邮件**与**相似性**值设置为**30%**。  
  
1.  在主页面中的**DQS 客户端**，单击**右箭头**旁边**供应商**知识基类，和选择**匹配策略**。  
  
     ![匹配在主菜单中的策略页](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "匹配在主菜单中的策略页")  
  
2.  上**映射**页上，选择**Excel 文件**为**数据源**。  
  
3.  单击**浏览**，确保该筛选器设置为**Excel 工作簿**，然后选择**清理供应商 List.xls**文件导出之后执行清理活动。  
  
    > [!NOTE]  
    >  在此活动结束时，您不能导出结果，因为此活动的主要目的是定义匹配策略。 您将为匹配活动创建一个数据质量项目，然后，您将在下一课中运行此项目以便使用此匹配策略从供应商列表中删除重复项。  
  
4.  映射**供应商 Id**列**供应商 ID**域，**供应商名称**列**供应商名称**域， **ContactEmailAddress**列**联系人电子邮件**域。 您仅需将源列映射到要用于定义匹配策略的域。 在这个例子中，您要使用 Supplier ID、Supplier Name 和 Contact Email 域来执行匹配策略活动。  
  
     ![映射的匹配策略定义过程的页](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "映射的匹配策略定义过程的页")  
  
5.  单击**下一步**将移到**匹配策略**其中你将定义一条规则匹配策略中的页。  
  
6.  单击**创建匹配规则**按钮在工具栏上的策略中创建规则。  
  
     ![创建匹配规则工具栏按钮](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "创建匹配规则工具栏按钮")  
  
7.  在**规则详细信息**在右侧窗格中输入**删除重复的供应商**为**规则名称**。  
  
8.  单击**添加新的域元素**右窗格中的工具栏中。  
  
     ![规则详细信息-添加一个新的域元素按钮](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "规则详细信息-添加一个新的域元素按钮")  
  
9. 选择**供应商 ID**为**域**和选择**先决条件**复选框。 请注意，**相似性**自动设置为**Exact**。 通过设置**供应商 ID**作为**先决条件**，指定两条记录中此字段的值必须返回 100%匹配，否则记录将不被视为匹配项和中的其他子句规则将忽略。  
  
     ![删除重复的供应商规则定义](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "删除重复的供应商规则定义")  
  
10. 单击**添加新的域元素**从工具栏上再次。  
  
11. 选择**供应商名称**域中，选择**类似**为**相似性**，和类型**70**为**权重**.  在这里，您指定供应商名称无需完全相同，但可以相似，以便将记录视作匹配。 权重指示该字段的分数对总匹配分数的贡献。  
  
12. 重复前面的两个步骤以添加**联系人电子邮件**域**30**为**权重**。  
  
13. 请注意，**最小匹配分数**设置为**80%**，这是你在中看到的值**常规**选项卡**配置**页**DQS 管理**。 您只能将此分数增加为高于此处的这个阈值。  
  
14. 请注意，**重叠群集**选项。 通过此选项，一条记录可以显示在多个群集中。 如果您将该设置为更改为“不重叠的群集”，则具有公共记录的多个群集将合并成单个群集。  
  
15. **启动**此页上的按钮允许您每个规则在策略中进行单独测试，而在下一页上开始按钮即可测试整个策略 （所有策略中的规则）。  
  
16. 单击**下一步**切换到**匹配结果**页。  
  
## <a name="next-step"></a>下一步  
 [任务 2：测试和发布匹配策略](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  