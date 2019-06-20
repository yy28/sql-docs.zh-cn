---
title: Analysis Services 教程补充课程：详细信息行 |Microsoft Docs
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
ms.openlocfilehash: bad45d18c351e838ec944b1ae67e3ce88c7e1d20
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263306"
---
# <a name="supplemental-lesson---detail-rows"></a>补充课程 - 详细信息行

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本补充课程中，使用 DAX 编辑器来定义自定义的详细信息行表达式。 详细信息行表达式是向最终用户提供有关度量值的聚合结果的详细信息的度量值的属性。 
  
估计的时间才能完成本课程中：**10 分钟**  
  
## <a name="prerequisites"></a>先决条件  

本文补充课程是表格建模教程的一部分。 执行任务之前在本补充课程中，应当已完成前面的课程或具有已完成的 Adventure Works Internet Sales 示例模型项目。  
  
## <a name="whats-the-issue"></a>问题是什么？

添加详细信息行表达式之前让我们看一下 InternetTotalSales 度量值的详细信息。

1.  在 SSDT 中，单击**模型**菜单 >**在 Excel 中的分析**打开 Excel 并创建一个空白数据透视表。
  
2.  在中**数据透视表字段**，添加**InternetTotalSales**到将 FactInternetSales 表中的度量值**值**， **CalendarYear**从对 DimDate 表**列**，并**EnglishCountryRegionName**到**行**。 该数据透视表将会按区域和年份 InternetTotalSales 度量值从提供的聚合的结果。 

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. 在数据透视表，双击针对某个年份和区域名称的聚合的值。 此处，双击针对澳大利亚和 2014 年的值。 将打开一个新工作表，其中包含数据，但不是有用的数据。

    ![as-lesson-detail-rows-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
我们希望看到这是一个包含参与 InternetTotalSales 度量值的聚合结果的数据的行和列的表。 为此，我们可以添加作为度量值的属性的详细信息行表达式。

## <a name="add-a-detail-rows-expression"></a>添加详细信息行表达式

#### <a name="to-create-a-detail-rows-expression"></a>若要创建详细信息行表达式 
  
1. 在 FactInternetSales 表的度量值网格中，单击**InternetTotalSales**度量值。 

2. 在中**属性** > **详细信息行表达式**，单击编辑器按钮以打开 DAX 编辑器。

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

    此表达式指定名称、 列和来自 FactInternetSales 表和相关的表的度量值结果将返回当用户双击数据透视表或报表中的聚合的结果。

4. 回到 Excel 中，删除在步骤 3 中创建的工作表，然后双击某个聚合的值。 这一次，度量值定义的详细信息行表达式属性，使用新工作表打开，其中包含很多有用的数据。

    ![as-lesson-detail-rows-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. 重新部署您的模型。

  
## <a name="see-also"></a>另请参阅  

[SELECTCOLUMNS 函数 (DAX)](/dax/selectcolumns-function-dax)  
[补充课程 - 动态安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[补充课程 - 不规则层次结构](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
