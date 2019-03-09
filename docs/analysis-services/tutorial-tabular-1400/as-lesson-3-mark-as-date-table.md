---
title: Analysis Services 教程第 3 课：标记为日期表 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 2008f066d537b1f88b9bf674c4a864217eae9890
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685564"
---
# <a name="mark-as-date-table"></a>标记为日期表

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在第 2 课：获取数据，导入名为的维度表**DimDate**。 虽然在模型中此表名为 DimDate，它可能也被称为*日期表*，它包含日期和时间数据。  
  
每当使用 DAX 时间智能函数，如当您创建度量值更高版本，必须指定属性包括*日期表*和唯一标识符*日期列*该表中。
  
在本课中，你将标记**DimDate**表格作为*日期表*并**日期**列 （在 Date 表中） 作为*日期列*（唯一标识符）。  

标记日期表和日期列之前，它是做一些调整以使您的模型更易于理解的好时机。 请注意，DimDate 表中名为的列**FullDateAlternateKey**。 此列的表中包含每个日历年中每一天中占一行。 在度量值公式和报表中大量使用此列。 但是，FullDateAlternateKey 实际上并不是本专栏的很好标识符。 为其重命名**日期**，使其更轻松地识别以及包括在公式中。 只要有可能，它是一个好办法重命名对象，如表和列，以使其更轻松地识别在 SSDT 和客户端报告应用程序中。 
  
学完本课的预计时间：**3 分钟**  
  
## <a name="prerequisites"></a>先决条件  

本文是表格建模教程应按顺序完成的一部分。 执行任务之前在本课程中，您应当已完成上一课：[第 2 课：获取数据](../tutorial-tabular-1400/as-lesson-2-get-data.md)。 

### <a name="to-rename-the-fulldatealternatekey-column"></a>若要重命名 FullDateAlternateKey 列

1.  在模型设计器中，单击**DimDate**表。

2.  双击的标头**FullDateAlternateKey**列中，然后将其重命名**日期**。

  
### <a name="to-set-mark-as-date-table"></a>标记为日期表  
  
1.  选择“日期”列，然后在“属性”窗口的“数据类型”下面确保已选中“日期”。  
  
2.  单击“表”菜单，然后依次单击“日期”和“标记为日期表”。  
  
3.  在“标记为日期表”对话框的“日期”列表框中，选择“日期”列作为唯一标识符。 默认情况下通常选择它。 单击“确定” 。 

    ![as-lesson3-date-table](../tutorial-tabular-1400/media/as-lesson3-date-table.png)
  

## <a name="whats-next"></a>下一步是什么？

[第 4 课：创建关系](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)。
  
