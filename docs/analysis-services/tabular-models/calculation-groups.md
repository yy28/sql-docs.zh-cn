---
title: Analysis Services 表格模型中的计算组 |Microsoft Docs
ms.date: 06/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: abc1f51d21613676fd94271f931e1a7692cc1efc
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822692"
---
# <a name="calculation-groups-preview"></a>计算组 （预览）
 
[!INCLUDE[ssas-appliesto-sql2019-aas](../../includes/ssas-appliesto-sql2019-aas.md)]

计算组可以显著减少冗余的度量值数由分组为常见的度量值表达式*计算项*。 Azure Analysis Services 中支持计算组和 SQL Server Analysis Services 2019 表格模型在 1470年及更高版本[兼容性级别](compatibility-level-for-tabular-models-in-analysis-services.md)。 1470 兼容性级别模型正处于**预览版**。  

本文介绍以下内容： 

> [!div class="checklist"]
> * 优势 
> * 计算组的工作原理
> * 动态格式字符串
> * 优先级
> * 工具
> * 限制



## <a name="benefits"></a>优势

计算组解决其中可能有的复杂模型中的问题为大量增生冗余使用相同的计算的使用时间智能计算最常见的度量值。 例如，销售分析人员想要查看总销售额，并按月至今的 (MTD)，每个季度结束日期 (QTD) 排序年度截止到现在 (YTD) 进行排序年度截止到现在为上一年 (PY) 等。 数据建模人员必须创建单独为每个计算，这可能会导致数十个度量值的度量值。 对于用户，这可以意味着无需通过许多度量值进行排序，并单独应用于其报表。 

让我们首先看一下计算组到 Power BI 等工具中的用户的显示方式。 然后，我们将看什么构成一个计算组中，并且它们如何创建在模型中。

计算组在报告客户端中作为具有单个列的表显示。 列不是像典型的列或维度，它表示一个或多个可重复使用计算，而是或*计算项*，可以应用于任何已添加到可视化效果的值筛选器的度量值。

在下面的动画中，用户正在分析 2012年和 2013 年销售数据。 应用计算组中，常见的基础度量值之前**销售**计算每个月的总销售额的总和。 然后，用户想要将应用时间智能计算，以获取销售总额的本月截止到现在，当季度至今本年截止到现在，依次类推。 不包括计算组中，用户将必须选择各个时间智能度量值。

与计算组，在此示例中名为**时间智能**，当用户拖动**时间计算**项**列**筛选区域中，每个计算项将显示为一个单独的列。 从基础度量值，计算每个行的值**销售**。  

![在 Power BI 中应用的计算组](media/calculation-groups/calc-groups-pbi.gif)


计算组使用**显式**DAX 度量值。 在此示例中，**销售**是已在模型中创建的显式度量值。 计算组不适用于隐式的 DAX 度量值。 例如，在 Power BI 中隐式度量值时创建用户将列拖到视觉对象来查看聚合的值，而无需创建显式度量值上。 在此期间，Power BI 生成为内联编写 DAX 计算-这意味着隐式度量值不能使用计算组的隐式度量值的 DAX。 引入了新的模型属性显示在表格对象模型 (TOM)， **DiscourageImplicitMeasures**。 目前，若要创建此属性的计算组必须设置为 **，则返回 true**。 如果设置为 true，Power BI Desktop 在 Live Connect 模式会禁用隐式度量值的创建。

## <a name="how-they-work"></a>它们的工作原理

现在，已了解如何计算组中受益的用户，让我们看一看如何创建显示的时间智能计算组示例。

了解详细信息之前，让我们引入了一些新的 DAX 函数专用于计算组： 

[SELECTEDMEASURE](https://docs.microsoft.com/dax/selectedmeasure-function-dax) -由表达式计算要引用的度量值的当前上下文中的项。 在此示例中，该 Sales 度量值。

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) -由计算项以确定是按名称的上下文中的度量值的表达式。

[ISSELECTEDMEASURE](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) -由计算项以确定在度量值的列表中指定的度量值的上下文中的表达式。

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax) -由要检索的度量值的上下文中的格式字符串的计算项的表达式。

### <a name="time-intelligence-example"></a>时间智能的示例

表名称-**时间智能**   
列名称-**时间计算**   
优先顺序- **20**   

#### <a name="time-intelligence-calculation-items"></a>时间智能计算项

**Current**

```dax
SELECTEDMEASURE()
```

**MTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESMTD(DimDate[Date]))
```

**QTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESQTD(DimDate[Date]))
```

**YTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

**PY**

```dax
CALCULATE(SELECTEDMEASURE(), SAMEPERIODLASTYEAR(DimDate[Date]))
```

**PY MTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "MTD"
)
```

**上一年度 QTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "QTD"
)
```

**PY YTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

**一年同期相比**

```dax
SELECTEDMEASURE() –
CALCULATE(
    SELECTEDMEASURE(),
    'Time Intelligence'[Time Calculation] = "PY"
)
```

**YOY%**

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

若要测试此计算组，可以执行 DAX 查询中 SSMS 或开放源代码[DAX Studio](http://daxstudio.org/)。 此查询示例中省略同比和增长率。

#### <a name="time-intelligence-query"></a>时间智能查询

```dax
EVALUATE
CALCULATETABLE (
    SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Current", CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "Current" ),
        "QTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "QTD" ),
        "YTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "YTD" ),
        "PY",      CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY" ),
        "PY QTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY QTD" ),
        "PY YTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY YTD" )
    ),
    DimDate[CalendarYear] IN { 2012, 2013 }
)
```

#### <a name="time-intelligence-query-return"></a>时间智能查询返回

返回下表显示为项应用每个计算的计算。 例如，可以看到 QTD 2012 年 3 月是年 1 月、 年 2 月和 2012 年 3 月的总和。

![返回的查询](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>动态格式字符串

*动态格式字符串*与计算组允许的度量值的格式字符串的条件性应用程序而无需强制他们返回的字符串。

表格模型支持通过使用 DAX 的动态格式度量值[格式](https://docs.microsoft.com/dax/format-function-dax)函数。 但是，格式函数有返回一个字符串，强制应数值也要返回以字符串形式的度量值的缺点。 这可能产生一些限制，如大多数 Power BI 视觉对象，具体取决于数字值，如图表中无法使用。

### <a name="dynamic-format-strings-for-time-intelligence"></a>时间智能的动态格式字符串

如果我们看一下时间智能示例如上所示，所有计算都项除外**增长率**应在上下文中使用当前度量值的格式。 例如， **YTD**计算的销售额基础度量值应为货币。 如果这是类似于订单基础度量值的计算组，格式应为数字。 **YOY %** ，但是，应该是基础度量值的百分比而不考虑格式。

有关**增长率**，我们可以通过格式字符串表达式属性设置为覆盖格式字符串**0.00%;-0.00%; 0.00%** 。 若要了解有关格式字符串表达式的属性的详细信息，请参阅[MDX 单元属性的格式字符串内容](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values)。

在 Power BI 中可视化此矩阵中，您将看到**销售当前/同比**并**订单当前/同比**保留它们各自的基础度量值的格式字符串。 **销售增长率**并**订单增长率**，但是，将覆盖要使用的格式字符串*百分比*格式。

![矩阵视觉对象中的时间智能](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>货币换算的动态格式字符串

动态格式字符串提供了简单的货币换算。 请考虑以下 Adventure Works 数据模型。 对于建模*一个多*货币换算定义的[换算类型](../currency-conversions-analysis-services.md#conversion-types)。

![表格模型中的货币速率](media/calculation-groups/calc-groups-currency-conversion.png)

一个**FormatString**列添加到**DimCurrency**表并填充其各自的货币的格式字符串。

![格式字符串列](media/calculation-groups/calc-groups-formatstringcolumn.png)

对于此示例中，以下的计算组然后定义为：

### <a name="currency-conversion-example"></a>货币转换示例

表名称-**货币换算**   
列名称-**转换计算**   
优先顺序- **5**   

#### <a name="calculation-items-for-currency-conversion"></a>为货币换算计算项

**不进行转换**

```dax
SELECTEDMEASURE()
```

**转换后的货币**

```dax
IF(
    //Check one currency in context & not US Dollar, which is the pivot currency:
    SELECTEDVALUE( DimCurrency[CurrencyName], "US Dollar" ) = "US Dollar",
    SELECTEDMEASURE(),
    SUMX(
        VALUES(DimDate[Date]),
        CALCULATE( DIVIDE( SELECTEDMEASURE(), MAX(FactCurrencyRate[EndOfDayRate]) ) )
    )
)
```

格式字符串表达式

```dax
SELECTEDVALUE(
    DimCurrency[FormatString],
    SELECTEDMEASUREFORMATSTRING()
)
```
格式字符串表达式必须返回标量的字符串。 使用新[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax)若要还原到的基础度量值的格式字符串，如果在筛选器上下文中有多种货币的函数。

下面的动画显示的动态格式货币换算**销售**在报表中的度量值。

![应用货币转换动态格式字符串](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>优先级

优先级是为计算组定义的属性。 多个计算组时，它指定计算的顺序。 较大的数字指示较高优先级，这意味着它将被计算之前计算组优先级较低。

对于此示例中，我们将为时间智能上述示例中，使用相同的模型，但还将添加**平均值**计算组。 平均值计算组包含是独立于传统的时间智能的它们不会发生的日期筛选器上下文-它们只是应用在其中平均计算的平均计算。

在此示例中，定义每日平均计算。 计算，例如平均每日的石油桶共有石油和天然气行业应用程序中。 其他常见的业务示例包括在零售中存储的平均销售额。

而此类计算计算独立于时间智能计算，很可能需要将它们合并。 例如，用户可能想要查看每日 YTD 若要查看从一年的某一开始为当前日期的每日石油率石油桶。 在此方案中，应计算项设置优先级。

### <a name="averages-example"></a>平均值示例

表名是**平均值**。   
列名称是**平均计算**。   
优先级**10**。   

#### <a name="calculation-items-for-averages"></a>计算平均值的项

**没有平均值**

```dax
SELECTEDMEASURE()
```

**每日平均**

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

下面是 DAX 查询和返回表的示例：

#### <a name="averages-query"></a>平均值查询

```dax
EVALUATE
    CALCULATETABLE (
        SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Sales", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "No Average"
        ),
        "YTD", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "No Average"
        ),
        "Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "Daily Average"
        ),
        "YTD Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "Daily Average"
        )
    ),
    DimDate[CalendarYear] = 2012
)
```

#### <a name="averages-query-return"></a>返回平均值查询

![返回的查询](media/calculation-groups/calc-groups-ytd-daily-avg.png)

下表显示了 2012 年 3 月值的计算方式。


|列名  |计算 |
|---------|---------|
|YTD     |    Feb、 Mar 2012 年 1 月的销售额的总和<br />= 495,364 + 506,994 + 373,483     |
|每日平均    |     2012 年 3 月的销售额除以 3 月天数<br />= 373,483 / 31       |
|YTD 每日平均     | 适用于 2012 年 3 月 YTD 除以 # 年 1 月、 年 2 月，日中的天数<br />=  1,375,841 / (31 + 29 + 31)       |

下面是应用的优先级的 YTD 计算项定义**20**。

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

下面是每日平均，应用具有的优先级**10**。

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

由于时间智能计算组的优先级高于平均值计算组，它是作为尽可能广泛应用。 YTD 每日平均计算适用于分子和分母 （数天） 的每日平均计算 YTD。

这相当于以下表达式：

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

此表达式：

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>横向递归

在上述时间智能示例中，计算项目中的某些引用其他相同的计算组中。 这称为*横向递归*。 例如，**增长率**将同时引用**同比**并**PY**。

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

在这种情况下，单独计算这两个表达式因使用不同计算语句。 不支持其他类型的递归。

## <a name="single-calculation-item-in-filter-context"></a>筛选器上下文中的单个计算项

在我们时间智能的示例中， **PY YTD**计算项都有一个计算表达式：

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

CALCULATE() 函数的 YTD 参数重写要重复使用已在 YTD 计算项中定义的逻辑的筛选器上下文。 不能将上一年度和 YTD 应用中的单个评估。 计算组是*仅应用*计算组中的单个计算项目是否在筛选器上下文。

## <a name="mdx-support"></a>MDX 支持

计算组支持多维表达式 (MDX) 查询。 这意味着，Microsoft Excel 用户，通过使用 MDX 的查询表格数据模型可以充分利用的工作表数据透视表中的计算组和图表。

## <a name="tools"></a>工具

计算组尚不支持在 SQL Server Data Tools，Visual Studio 中使用 Analysis Services 扩展插件。 但是，可以通过使用表格模型脚本语言 (TMSL) 或开放源代码创建计算组[表格编辑器](https://github.com/otykier/TabularEditor)。

## <a name="limitations"></a>限制

[对象级别安全](object-level-security.md)(OLS) 定义计算上不支持组的表。 但是，可以在相同的模型中的其他表上定义 OLS。 如果计算项引用 OLS 受保护的对象，则返回一般错误。

[行级别安全性](roles-ssas-tabular.md#bkmk_rowfliters)(RLS) 不受支持。 （直接或间接），可以对表中相同的模型，但不是在计算组本身定义 RLS。

[详细信息行表达式](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)计算组不支持。

## <a name="see-also"></a>另请参阅  

[表格模型中的 DAX](understanding-dax-in-tabular-models-ssas-tabular.md)   
[DAX 参考](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  
