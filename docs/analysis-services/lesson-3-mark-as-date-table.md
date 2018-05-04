---
title: 第 4 课： 将标记为日期表 |Microsoft 文档
ms.custom: ''
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 08a3e1852f58e1f21049d1a5c0551669423845db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-3-mark-as-date-table"></a>第 3 课： 将标记为日期表
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在“第 2 课：添加数据”中，您导入了名为 DimDate 的维度表。 虽然您的模型中此表的名称为 DimDate，它可以也被称为*日期表*，因为它包含日期和时间数据。  
  
每当像将你创建的度量值稍有更高版本时，可以在计算中使用 DAX 时间智能函数，你必须指定日期表属性，其中包括*日期表*和唯一标识符*日期列*该表中。
  
在本课程中，您将标记为 DimDate 表*日期表*和日期列 （在日期表中） 作为*日期列*（唯一标识符）。  

我们将标记为日期表和日期列之前，我们需要执行少量的管理，以便更轻松地了解我们的模型。 你会注意到 DimDate 表中一个名为列**FullDateAlternateKey**。 它包含在表中每个日历年中每一天中占一行。 我们将使用此列很多在度量值公式和报表中。 但是，FullDateAlternateKey 实际上不是此列的良好标识符。 我们将其重命名为**日期**，使其更轻松地识别和在公式中包含。 只要有可能，它是重命名对象，如表和列，以使它们更轻松地标识客户端报告应用程序，如 Power BI 和 Excel 中的一个好办法。 
  
学完本课的估计时间： **3 分钟**  
  
## <a name="prerequisites"></a>必要條件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 之前在本课程中执行任务，你应完成上一课：[第 2 课： 添加数据](../analysis-services/lesson-2-add-data.md)。 

### <a name="to-rename-the-fulldatealternatekey-column"></a>若要重命名 FullDateAlternateKey 列

1.  在模型设计器中，单击**DimDate**表。

2.  双击的标头**FullDateAlternateKey**列，然后将其命名为和**日期**。

  
### <a name="to-set-mark-as-date-table"></a>标记为日期表  
  
1.  选择“日期”列，然后在“属性”窗口的“数据类型”下面确保已选中“日期”。  
  
2.  单击“表”菜单，然后依次单击“日期”和“标记为日期表”。  
  
3.  在“标记为日期表”对话框的“日期”列表框中，选择“日期”列作为唯一标识符。 默认情况下将通常选择该功能。 单击 **“确定”**。 

    ![作为表格-lesson3-日期的表](../analysis-services/media/as-tabular-lesson3-date-table.png)
  

## <a name="whats-next"></a>下一步是什么？
转到下一课：[第 4 课： 创建关系](../analysis-services/lesson-4-create-relationships.md)。
  
