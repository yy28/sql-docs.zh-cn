---
title: 第 9 课创建透视 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e917e817768571e1959ae6163743ecdad0409af
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38031615"
---
# <a name="lesson-8-create-perspectives"></a>第 8 课： 创建透视
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课程中，您将创建 Internet Sales 透视。 透视可定义模型的可查看子集，借此您可以将注意力集中在特定业务或特定应用程序上。 当用户使用透视连接到模型时，他们只能看到那些模型对象 （表、 列、 度量值、 层次结构和 Kpi） 作为该透视中定义的字段。  
  
在本课中创建的 Internet Sales 透视将排除 DimCustomer 表对象。 当您创建排除视图中某些对象的透视时，这些对象仍然存在于模型中；但是，它们在报表客户端字段列表中不可见。 无论计算列和度量值是否包含在透视中，都仍可以通过排除的对象数据进行计算。  
  
本课程的目的是介绍如何创建透视以及如何逐步熟悉表格模型创作工具。 如果您以后扩展此模型以包括其他表，可以创建其他透视以定义不同视点的模型，例如，库存和销售额。 若要了解详细信息，请参阅[透视](../analysis-services/tabular-models/perspectives-ssas-tabular.md)。  
  
学完本课的估计时间： **5 分钟**  
  
## <a name="prerequisites"></a>必要條件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 在之前在本课程中执行的任务，您应已完成上一课：[第 7 课： 创建关键绩效指标](../analysis-services/lesson-7-create-key-performance-indicators.md)。  
  
## <a name="create-perspectives"></a>创建透视  
  
#### <a name="to-create-an-internet-sales-perspective"></a>创建“Internet Sales”透视  
  
1.  单击**模型**菜单 >**透视** > **创建和管理**。  
  
2.  在“透视”对话框中，单击“新建透视”。  
  
3.  双击**新的透视**列标题，然后重命名**Internet Sales**。  
  
4.  选择表的所有*除* **DimCustomer**。  
  
    ![作为-表格-lesson8-透视](../analysis-services/media/as-tabular-lesson8-perspectives.png)
  
    在后面的课程中，你将在 Excel 功能中使用分析来测试此透视。 Excel 数据透视表字段列表将包括除 DimCustomer 表之外的每个表。  

## <a name="whats-next"></a>下一步是什么？
转到下一课：[第 9 课： 创建层次结构](../analysis-services/lesson-9-create-hierarchies.md)。
  
  
  
  
