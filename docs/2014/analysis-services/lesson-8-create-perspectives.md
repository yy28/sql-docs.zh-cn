---
title: Lesson 9： 创建透视 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: fe2e746ec290aeb3b8690f818875616f2b9dd2f1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128210"
---
# <a name="lesson-9-create-perspectives"></a>第 9 课：创建透视
  在本课程中，您将创建 Internet Sales 透视。 透视可定义模型的可查看子集，借此您可以将注意力集中在特定业务或特定应用程序上。 当用户使用透视连接到模型时，将只能看到与该透视中定义的字段相同的那些模型对象（表、列、度量值、层次结构和 KPI）。  
  
 本课中创建的 Internet Sales 透视将排除 Customer 表对象。 当您创建排除视图中某些对象的透视时，这些对象仍然存在于模型中；但是，它们在报表客户端字段列表中不可见。 无论计算列和度量值是否包含在透视中，都仍可以通过排除的对象数据进行计算。  
  
 本课程的目的是介绍如何创建透视以及如何逐步熟悉表格模型创作工具。 如果您以后扩展此模型以包含其他表，则可以创建其他透视以定义不同的模型视点，例如 Inventory 和 Sales Force。  
  
 若要了解详细信息，请参阅[透视表（SSAS 表格）](tabular-models/perspectives-ssas-tabular.md)。  
  
 学完本课的估计时间： **5 分钟**  
  
## <a name="prerequisites"></a>必要條件  
 本主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本课程中的任务之前，应该已完成上一课：[第 8 课：创建关键绩效指标](lesson-7-create-key-performance-indicators.md)。  
  
## <a name="create-perspectives"></a>创建透视  
  
#### <a name="to-create-an-internet-sales-perspective"></a>创建“Internet Sales”透视  
  
1.  在模型设计器中，单击**模型**菜单，，然后单击**透视**。  
  
2.  在“透视”对话框中，单击“新建透视”。  
  
3.  若要重命名该透视，请双击**新透视 1**列标题，然后键入`Internet Sales`。  
  
4.  在**字段**，选择以下表**日期**， **Geography**，**产品**，**产品类别**，**产品子类别**，和`Internet Sales`。  
  
     请注意，您从此透视中排除了 Customer 表及其所有列。 稍后，您将在第 12 课中使用“在 Excel 中分析”功能来测试此透视。 Excel 数据透视表字段列表将包含除 Customer 表之外的所有表。  
  
5.  验证所做的选择，确保未选中“Customer”表，然后单击“确定”  
  
## <a name="next-steps"></a>后续步骤  
 若要继续学习本教程，请转到下一课：[第 10 课：创建层次结构](lesson-9-create-hierarchies.md)。  
  
  