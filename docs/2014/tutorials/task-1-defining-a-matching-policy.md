---
title: 任务 1：定义匹配策略 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6f89a720-fce5-4f60-bef3-a159bbc9f25c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 85a6ca52573bec3d7e6c19e68f809048ed0786db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222798"
---
# <a name="task-1-defining-a-matching-policy"></a>任务 1：定义匹配策略
  在本任务中，您将创建含有一个规则的匹配策略。 该规则具有一个先决条件：**供应商 ID**，这意味着在使用在规则中的其他域之前 Supplier Id 必须匹配。 该规则使用其他两个域：**供应商名称**与**相似性**值设置为**70%** 并**联系人电子邮件**与**相似性**值设置为**30%**。  
  
1.  在主页面中的**DQS 客户端**，单击**右箭头**旁边**供应商**知识，然后选择**匹配策略**。  
  
     ![匹配策略在主菜单中的页](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "匹配在主菜单中的策略页")  
  
2.  上**地图**页上，选择**Excel 文件**有关**数据源**。  
  
3.  单击**浏览**，请确保该筛选器设置为**Excel 工作簿**，然后选择**Cleansed Supplier List.xls**文件执行清理活动后导出。  
  
    > [!NOTE]  
    >  在此活动结束时，您不能导出结果，因为此活动的主要目的是定义匹配策略。 您将为匹配活动创建一个数据质量项目，然后，您将在下一课中运行此项目以便使用此匹配策略从供应商列表中删除重复项。  
  
4.  映射**SupplierID**列**Supplier ID**域， **Supplier Name**列**Supplier Name**域， **ContactEmailAddress**列添加到**联系人电子邮件**域。 您仅需将源列映射到要用于定义匹配策略的域。 在这个例子中，您要使用 Supplier ID、Supplier Name 和 Contact Email 域来执行匹配策略活动。  
  
     ![映射页的匹配策略定义过程](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "映射页的匹配策略定义过程")  
  
5.  单击**下一步**转为**匹配策略**，您将定义一条规则的匹配策略中的页。  
  
6.  单击**创建匹配规则**按钮在工具栏上的策略中创建规则。  
  
     ![创建匹配规则工具栏按钮](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "创建匹配规则工具栏按钮")  
  
7.  在中**规则的详细信息**在右侧窗格中输入**删除重复供应商**有关**规则名称**。  
  
8.  单击**添加新的域元素**在右窗格的工具栏中。  
  
     ![规则详细信息-添加新的域元素按钮](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "规则详细信息-添加新的域元素按钮")  
  
9. 选择**供应商 ID**有关**域**，然后选择**先决条件**复选框。 请注意，**相似性**将自动设置为**Exact**。 通过设置**供应商 ID**作为**先决条件**，指定此字段中的两个记录的值必须返回 100%匹配，否则记录将不被视为匹配项和中的其他子句规则将被忽略。  
  
     ![删除重复的供应商规则定义](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "中删除重复的供应商规则定义。")  
  
10. 单击**添加新的域元素**从工具栏中再次。  
  
11. 选择**Supplier Name**该域，选择**类似**的**相似性**，然后键入**70**为**权重**.  在这里，您指定供应商名称无需完全相同，但可以相似，以便将记录视作匹配。 权重指示该字段的分数对总匹配分数的贡献。  
  
12. 重复前两个步骤以添加**联系人电子邮件**具有域**30**有关**权重**。  
  
13. 请注意，**最小匹配分数**设置为**80%**，这是您在中看到的值**常规**选项卡**配置**页**DQS 管理**。 您只能将此分数增加为高于此处的这个阈值。  
  
14. 请注意，**重叠的群集**选择选项。 通过此选项，一条记录可以显示在多个群集中。 如果您将该设置为更改为“不重叠的群集”，则具有公共记录的多个群集将合并成单个群集。  
  
15. **启动**此页上的按钮，可单独测试策略中的每个规则而在下一页中的开始按钮可以测试整个策略 （所有策略中的规则）。  
  
16. 单击**下一步**若要切换到**匹配结果**页。  
  
## <a name="next-step"></a>下一步  
 [任务 2:测试和发布匹配策略](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  
