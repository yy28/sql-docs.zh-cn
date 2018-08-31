---
title: 第 3 课： 标记为日期表 |Microsoft Docs
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7cb63b6cb67303dd763263b7d9dbeea30cfc4e3b
ms.sourcegitcommit: e8e013b4d4fbd3b25f85fd6318d3ca8ddf73f31e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42791978"
---
# <a name="lesson-3-mark-as-date-table"></a>第 3 课：标记为日期表
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在“第 2 课：添加数据”中，您导入了名为 DimDate 的维度表。 虽然在模型中此表名为 DimDate，它可能也被称为*日期表*，它包含日期和时间数据。  
  
每当在计算中使用 DAX 时间智能函数作为将您创建度量值稍有更高版本时，必须指定日期表属性，其中包括*日期表*和唯一标识符*日期列*该表中。
  
在本课中，您将 DimDate 表标记为*日期表*和日期列 （在 Date 表中） 作为*日期列*（唯一标识符）。  

我们将标记日期表和日期列之前，我们需要做一些调整以使我们的模型更易于理解。 您会注意到，DimDate 表中名为的列**FullDateAlternateKey**。 它包括在表中每个日历年中每一天中占一行。 我们将使用此列很多在度量值公式和报表中。 但是，FullDateAlternateKey 实际上不是本专栏的很好标识符。 我们将其重命名为**日期**，使其更轻松地识别以及包括在公式中。 只要有可能，它是重命名对象，如表和列，以使其更轻松地标识客户端报告应用程序，如 Power BI 和 Excel 中的一个好办法。 
  
学完本课的估计时间： **3 分钟**  
  
## <a name="prerequisites"></a>必要條件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 在之前在本课程中执行的任务，您应已完成上一课：[第 2 课： 添加数据](../analysis-services/lesson-2-add-data.md)。 

### <a name="to-rename-the-fulldatealternatekey-column"></a>若要重命名 FullDateAlternateKey 列

1.  在模型设计器中，单击**DimDate**表。

2.  双击的标头**FullDateAlternateKey**列中，然后将其重命名**日期**。

  
### <a name="to-set-mark-as-date-table"></a>标记为日期表  
  
1.  选择“日期”列，然后在“属性”窗口的“数据类型”下面确保已选中“日期”。  
  
2.  单击“表”菜单，然后依次单击“日期”和“标记为日期表”。  
  
3.  在“标记为日期表”对话框的“日期”列表框中，选择“日期”列作为唯一标识符。 它通常是默认选中状态。 单击“确定” 。 

    ![作为表格-lesson3-日期-表](../analysis-services/media/as-tabular-lesson3-date-table.png)
  

## <a name="whats-next"></a>下一步是什么？
转到下一课：[第 4 课： 创建关系](../analysis-services/lesson-4-create-relationships.md)。
  
