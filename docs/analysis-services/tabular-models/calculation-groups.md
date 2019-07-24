---
title: Analysis Services 表格模型中的计算组 |Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: af63f41555a021fc720c7d1e15778265fe7de500
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419524"
---
# <a name="calculation-groups-preview"></a>计算组 (预览)
 
[!INCLUDE[ssas-appliesto-sql2019-aas](../../includes/ssas-appliesto-sql2019-aas.md)]

计算组可以通过将常见度量值表达式分组为*计算项*来大幅减少冗余度量值的数量。 在1470和更高的[兼容级别](compatibility-level-for-tabular-models-in-analysis-services.md)Azure Analysis Services 和 SQL Server Analysis Services 2019 表格模型支持计算组。 1470兼容级别的模型目前处于**预览**状态。  

本文介绍以下内容： 

> [!div class="checklist"]
> * 优势 
> * 计算组的工作方式
> * 动态格式字符串
> * 排序
> * 优先级
> * 工具
> * 限制



## <a name="benefits"></a>优势

计算组解决了复杂模型中的问题, 在这种模型中, 可以使用相同的计算 (最常见的时间智能计算) 来增加冗余度量值。 例如, 销售分析人员想要按月份截止日期 (MTD)、季度截止到现在 (QTD)、年初至今 (YTD)、本年迄今订单 (PY) 等来查看销售总额和订单, 等等。 数据建模器必须为每个计算创建单独的度量值, 这可能会导致多个度量值。 对于用户而言, 这可能意味着必须按多个度量值进行排序, 并将它们分别应用到报表中。 

首先, 让我们看一下如何在 Power BI 的报表工具中向用户显示计算组。 接下来, 我们将介绍如何组成计算组, 以及如何在模型中创建计算组。

计算组在报告客户端中作为具有单个列的表显示。 列不像典型的列或维度, 而是表示一个或多个可重复使用的计算, 或可应用于已添加到可视化效果的值筛选器的任何度量值的*计算项*。

在下面的动画中, 用户正在分析销售数据2012年和2013年。 在应用计算组之前, 通用基础度量值**销售额**计算每月总销售额的总和。 然后, 用户需要应用时间智能计算, 以获取本月至今、季度截止到目前、本年迄今等的销售总额。 如果没有计算组, 则用户必须选择单个时间智能度量值。

对于计算组, 在此示例中, 在名为**Time 情报**的情况下, 当用户将**时间计算**项拖到 "**列**" 筛选区域时, 每个计算项都显示为一个单独的列。 每行的值都是从基本度量值**Sales**计算得出的。  

![正在应用 Power BI 的计算组](media/calculation-groups/calc-groups-pbi.gif)


计算组使用**显式**DAX 度量值。 在此示例中, **Sales**是已在模型中创建的显式度量值。 计算组不能与隐式 DAX 度量值一起使用。 例如, 在 Power BI 隐式度量值是在用户将列拖动到视觉对象上以查看聚合值时创建的, 而无需创建显式度量值。 目前, Power BI 为作为内联 DAX 计算编写的隐式度量值生成 DAX-这意味着隐式度量值不能与计算组一起使用。 已在表格对象模型 (TOM) 中看到一个新的模型属性, **DiscourageImplicitMeasures**。 目前, 若要创建计算组, 必须将此属性设置为**true**。 如果设置为 true, 则在 "实时连接" 模式下 Power BI Desktop 将禁用隐式度量值的创建。

## <a name="how-they-work"></a>工作原理

现在, 你已了解计算组如何使用户受益, 接下来让我们看看如何创建显示的 "时间智能计算组" 示例。

在深入了解详细信息之前, 让我们先介绍一些用于计算组的新 DAX 函数: 

[SELECTEDMEASURE](https://docs.microsoft.com/dax/selectedmeasure-function-dax) -用于计算项以引用当前上下文中的度量值的表达式。 在此示例中, 为 "销售额" 度量值。

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) -用于计算项的表达式, 用来确定上下文中按名称的度量值。

[ISSELECTEDMEASURE](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) -用于计算项的表达式, 用来确定在度量值列表中指定的度量值。

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax) -用于计算项的表达式, 用来检索位于上下文中的度量值的格式字符串。

### <a name="time-intelligence-example"></a>时间智能示例

表名-**时间智能**   
列名-**时间计算**   
优先级- **20**   

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

**PY QTD**

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

**同比变化率**

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

若要测试此计算组, 可以在 SSMS 或开源[DAX Studio](http://daxstudio.org/)中执行 DAX 查询。 此查询示例中省略了同比变化率和同比变化率%。

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

返回表显示应用的每个计算项的计算。 例如, 你可以看到三月2012的 QTD 是2月到2月到 2012 3 月的总和。

![查询返回](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>动态格式字符串

带有计算组的*动态格式字符串*允许将格式字符串的条件应用应用于度量值, 而无需强制它们返回字符串。

表格模型通过使用 DAX 的[FORMAT](https://docs.microsoft.com/dax/format-function-dax)函数支持度量值的动态格式设置。 但是, FORMAT 函数的缺点是返回一个字符串, 并强制执行其他为数字的度量值, 并将其作为字符串返回。 这可能会有一些限制, 例如不能使用大多数 Power BI 视觉对象, 具体取决于数值, 如图表。

### <a name="dynamic-format-strings-for-time-intelligence"></a>用于时间智能的动态格式字符串

如果我们看一下上面所示的时间智能示例, 则除**同比变化率%** 之外的所有计算项应在上下文中使用当前度量值的格式。 例如, 在销售基准度量值上计算的**YTD**应为货币。 如果这是一个计算组, 而这种计算组类似于 Orders 基本度量值, 则格式将为数值。 不过,**同比变化率%** 应为百分比, 而不考虑基础度量值的格式。

对于**同比变化率%** , 我们可以通过将格式字符串表达式属性设置为**0.00%;-0.00%; 0.00%** , 来覆盖格式字符串。 若要详细了解格式字符串表达式属性, 请参阅[MDX 单元属性-格式字符串内容](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values)。

在 Power BI 中的此矩阵视觉对象中, 你会看到**Sales current/同比变化率**和**ORDERS 当前/同比变化率**保留各自的基本度量值格式字符串。 不过, **SALES 同比变化率%** 和**Orders 同比变化率%** 将覆盖格式字符串以使用*百分比*格式。

![矩阵视觉对象中的时间智能](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>用于货币换算的动态格式字符串

动态格式字符串提供了简单的货币换算。 请考虑以下艾德作品数据模型。 它*针对*[转换类型](../currency-conversions-analysis-services.md#conversion-types)定义的一对多货币换算建模。

![表格模型中的货币费率](media/calculation-groups/calc-groups-currency-conversion.png)

"格式字符串 **" 列将**添加到**DimCurrency**表中, 并使用各自货币的格式字符串填充。

![格式字符串列](media/calculation-groups/calc-groups-formatstringcolumn.png)

在此示例中, 将以下计算组定义为:

### <a name="currency-conversion-example"></a>货币换算示例

表名称-**货币换算**   
列名称-**转换计算**   
优先级- **5**   

#### <a name="calculation-items-for-currency-conversion"></a>用于货币换算的计算项

**无转换**

```dax
SELECTEDMEASURE()
```

**转换货币**

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
格式字符串表达式必须返回标量字符串。 如果筛选器上下文中有多个货币, 则使用新的[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax)函数恢复为基本度量值格式字符串。

以下动画显示了报表中**销售**度量值的动态格式货币转换。

![应用的货币换算动态格式字符串](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>优先级

优先级是为计算组定义的属性。 它指定了多个计算组时的计算顺序。 数字越大, 表示优先级越高, 这意味着在优先级较低的计算组之前计算。

在此示例中, 我们将使用与上述时间智能示例相同的模型, 同时添加**平均**计算组。 平均计算组包含与传统时间智能无关的平均计算, 因为它们不会更改日期筛选器上下文, 它们只会在其中应用平均计算。

在此示例中, 将定义每日平均计算。 对于石油和天然气应用程序而言, 一般的计算 (例如每日的 barrels) 都很常见。 其他常见业务示例包含零售的商店销售平均值。

虽然这种计算是独立于时间智能计算计算的, 但也有可能需要将它们组合在一起。 例如, 用户可能想要查看 YTD 的 barrels, 以查看从该年开始到当前日期的每日燃油费率。 在此方案中, 应为计算项设置优先级。

### <a name="averages-example"></a>平均示例

表名称为**平均值**。   
列名为**平均计算**。   
优先级为**10**。   

#### <a name="calculation-items-for-averages"></a>计算平均值的项

**无平均值**

```dax
SELECTEDMEASURE()
```

**每日平均**

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

下面是 DAX 查询和返回表的示例:

#### <a name="averages-query"></a>平均查询

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

#### <a name="averages-query-return"></a>平均查询返回

![查询返回](media/calculation-groups/calc-groups-ytd-daily-avg.png)

下表显示了如何计算三月2012的值。


|列名  |计算 |
|---------|---------|
|YTD     |    Jan, 二月, 三月2012的销售总额<br />= 495364 + 506994 + 373483     |
|每日平均    |     三月2012的销售额除以3月份的天数<br />= 373483/31       |
|每日 YTD 平均值     | 三月2012的 YTD 除以一月、二月和三月的天数<br />= 1375841/(31 + 29 + 31)       |

下面是已应用优先级为**20**的 YTD 计算项的定义。

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

下面是应用优先级为**10**的每日平均值。

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

由于时间智能计算组的优先级高于平均计算组的优先级, 因此它会尽可能广泛地应用。 YTD 每日平均计算同时应用于每日平均计算的分子和分母 (天数的计数)。

这等效于以下表达式:

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

不是此表达式:

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>侧向递归

在上述时间智能示例中, 某些计算项引用相同计算组中的其他项。 这称为 "*侧向递归*"。 例如,**同比变化率%** 引用**同比变化率**和**PY**。

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

在这种情况下, 这两个表达式是单独计算的, 因为它们使用的是不同的计算语句。 不支持其他类型的递归。

## <a name="single-calculation-item-in-filter-context"></a>筛选上下文中的单个计算项

在我们的时间智能示例中, **PY YTD**计算项具有一个计算表达式:

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

计算 () 函数的 YTD 参数重写筛选器上下文, 以重用已在 YTD 计算项中定义的逻辑。 不能将 PY 和 YTD 应用于单个评估中。 仅当计算组中的单个计算项在筛选器上下文中时,*才应用*计算组。

## <a name="mdx-support"></a>MDX 支持

计算组支持多维数据表达式 (MDX) 查询。 这意味着, 通过使用 MDX 查询表格数据模型的 Microsoft Excel 用户可充分利用工作表数据透视表和图表中的计算组。

## <a name="tools"></a>工具

在 SQL Server Data Tools 中, 不支持计算组 Analysis Services 扩展。 但是, 可以通过使用表格模型脚本语言 (TMSL) 或开源[表格编辑器](https://github.com/otykier/TabularEditor)来创建计算组。

## <a name="limitations"></a>限制

[对象级别安全性](object-level-security.md)不支持在计算组表中定义 (OLS)。 但是, 可以在同一模型中的其他表上定义 OLS。 如果计算项指的是 OLS 保护的对象, 则会返回一般错误。

[行级别安全性](roles-ssas-tabular.md#bkmk_rowfliters)(RLS) 不受支持。 您可以在同一模型中的表上定义 RLS, 但不能对计算组本身 (直接或间接) 定义 RLS。

## <a name="see-also"></a>请参阅  

[表格模型中的 DAX](understanding-dax-in-tabular-models-ssas-tabular.md)   
[DAX 参考](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  
