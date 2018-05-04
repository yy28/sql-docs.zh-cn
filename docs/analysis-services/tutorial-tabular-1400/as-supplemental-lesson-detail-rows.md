---
title: Analysis Services 教程补充课程： 详细信息行 |Microsoft 文档
description: 描述如何创建在 Analysis Services 教程的详细信息行表达式。
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 16388c1753671e9b835325535685e1d9324e9b52
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="supplemental-lesson---detail-rows"></a>补充课程-详细信息行

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在此补充课程中，你可以使用 DAX 编辑器来定义自定义的详细信息行表达式。 详细信息行表达式是对度量值，属性提供有关度量值的聚合结果的详细信息的最终用户。 
  
学完本课的估计时间：**10 分钟**  
  
## <a name="prerequisites"></a>必要條件  

补充课程本文是表格建模教程的一部分。 之前在本课程中补充执行任务，你应完成前面的课程中所有或具有已完成的 Adventure Works Internet Sales 示例模型项目。  
  
## <a name="whats-the-issue"></a>问题是什么？

我们来看的详细信息的 InternetTotalSales 度量值，然后再添加详细信息行表达式。

1.  在 SSDT 中，单击**模型**菜单 >**在 Excel 中的分析**先打开 Excel 并创建一个空白数据透视表。
  
2.  在**数据透视表字段**，添加**InternetTotalSales**从 FactInternetSales 表的度量值**值**， **CalendarYear**从 DimDate 表**列**，和**EnglishCountryRegionName**到**行**。 数据透视表现在提供 InternetTotalSales 度量值按区域和年份中的聚合的结果。 

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. 在数据透视表，每一年和区域名称双击聚合的值。 此处我们双击澳大利亚和 2014年的年份的值。 将打开新工作表，其中包含数据，但不是有用的数据。

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
我们希望看到下面是包含的贡献 InternetTotalSales 度量值的聚合结果的数据行和列的表。 若要做到这一点，我们可以添加作为度量值的属性的详细信息行表达式。

## <a name="add-a-detail-rows-expression"></a>添加详细信息行表达式

#### <a name="to-create-a-detail-rows-expression"></a>若要创建详细信息行表达式 
  
1. 在 FactInternetSales 表的度量值网格中，单击**InternetTotalSales**度量值。 

2. 在**属性** > **详细信息行表达式**，单击编辑器按钮以打开 DAX 编辑器。

    ![as-lesson-detail-rows-ellipse](../tutorial-tabular-1400/media/as-lesson-detail-rows-ellipse.png)

3. 在 DAX 编辑器中，输入以下表达式：

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    此表达式指定名称列，并当用户双击的数据透视表或报表中的某个聚合的结果会返回从 FactInternetSales 表和相关的表的度量值结果。

4. 返回在 Excel 中，删除在步骤 3 中创建的表，然后双击聚合的值。 此时，定义度量值的详细信息行表达式属性，使用的新工作表打开，其中包含很多有用的数据。

    ![as-lesson-detail-rows-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. 重新部署您的模型。

  
## <a name="see-also"></a>另请参阅  

[SELECTCOLUMNS 函数 (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)  
[补充课程 - 动态安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[补充课程 - 不规则层次结构](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
