---
title: PredictTimeSeries （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ff8525e9742009e5a5ada680160f20d5e8063d86
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363517"
---
# <a name="predicttimeseries-dmx"></a>PredictTimeSeries (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  返回时序数据的未来预测值。 时序数据是连续的，可以存储在嵌套表或事例表中。 **PredictTimeSeries**函数始终返回嵌套表。  
  
## <a name="syntax"></a>语法  
  
```  
  
PredictTimeSeries(<table column reference>)  
PredictTimeSeries(<table column reference>, n)  
PredictTimeSeries(<table column reference>, n-start, n-end)  
PredictTimeSeries(<scalar column reference>)  
PredictTimeSeries(<scalar column reference>, n)  
PredictTimeSeries(<scalar column reference>, n-start, n-end)  
PredictTimeSeries(<table column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<table column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
```  
  
## <a name="arguments"></a>自变量  
 *\<table column reference>*, *\<scalar column referenc>*  
 指定要预测的列的名称。 列可以包含标量数据或表格格式数据。  
  
 *n*  
 指定要预测的后续步长数。 如果没有为*n*指定值，则默认值为1。  
  
 *n*不能为0。 如果没有执行过至少一次预测，则函数将返回一个错误。  
  
 *n-开始，n-结束*  
 指定时序步长的范围。  
  
 *n-start*必须是整数且不能为0。  
  
 *n end*必须是大于*n 开头的*整数。  
  
 *\<source query>*  
 定义用于进行预测的外部数据。  
  
 REPLACE_MODEL_CASES | EXTEND_MODEL_CASES  
 指示如何处理新数据。  
  
 REPLACE_MODEL_CASES 指定应使用新数据替换模型中的数据点。 但是，预测基于现有挖掘模型中的模式。  
  
 EXTEND_MODEL_CASES 指定应将新数据添加到原始定型数据集。 仅在新数据已用完之后才根据组合的数据集执行未来预测。  
  
 这些参数仅在使用 PREDICTION JOIN 语句添加新数据时才可用。 如果使用 PREDICTION JOIN 查询并且没有指定参数，则默认值为 EXTEND_MODEL_CASES。  
  
## <a name="return-type"></a>返回类型  
 \<*table expression*>。  
  
## <a name="remarks"></a>备注  
 当使用 PREDICTION JOIN 语句添加新数据时，[!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法不支持历史预测。  
  
 在 PREDICTION JOIN 中，预测过程总是从原始定型系列的末尾之后的时间步长立即开始。 即使您添加新的数据也是如此。 因此， *n*参数和*n 启动*参数值必须是大于0的整数。  
  
> [!NOTE]  
>  新数据的长度不影响预测起点。 因此，如果您想要添加新数据并且还要执行新预测，请确保将预测起点设置为大于新数据的长度的值，或者按照新数据的长度来扩展预测终点。  
  
## <a name="examples"></a>示例  
 下面的示例显示如何对现有的时序模型执行预测：  
  
-   第一个示例显示如何根据当前模型执行指定次数的预测。  
  
-   第二个示例显示如何使用 REPLACE_MODEL_CASES 参数将指定模型中的模式应用到新的数据集。  
  
-   第三个示例显示如何使用 EXTEND_MODEL_CASES 参数用最新数据更新挖掘模型。  
  
 若要了解有关使用时序模型的详细信息，请参阅数据挖掘教程[第2课： &#40;中级数据挖掘教程&#41;](https://msdn.microsoft.com/library/9a988156-c900-4c22-97fa-f6b0c1aea9e2)和[时序预测 DMX 教程](https://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2)。  
  
> [!NOTE]  
>  您可能会从模型中获取不同的结果；下面提供的示例结果仅用于说明结果格式。  
  
### <a name="example-1-predicting-a-number-of-time-slices"></a>示例 1：预测时间段数  
 下面的示例使用**PredictTimeSeries**函数返回下三个时间步长的预测，并将结果限制为欧洲和太平洋地区的 M200 系列。 在此特定模型中，可预测属性是数量，因此您必须使用 `[Quantity]` 作为 PredictTimeSeries 函数的第一个参数。  
  
```  
SELECT FLATTENED  
    [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity],3)AS t   
FROM  
    [Forecasting]  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 Pacific'  
```  
  
 预期的结果：  
  
|Model Region|t.$TIME|t.Quantity|  
|------------------|-------------|----------------|  
|M200 Europe|7/25/2008 12:00:00 AM|121|  
|M200 Europe|8/25/2008 12:00:00 AM|142|  
|M200 Europe|9/25/2008 12:00:00 AM|152|  
|M200 Pacific|7/25/2008 12:00:00 AM|46|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|42|  
  
 在此示例中使用了 FLATTENED 关键字，目的是使结果更易于读取。  如果不使用 FLATTENED 关键字，而返回一个分层行集，此查询将返回两列。 第一列包含 [ModelRegion] 的值，第二列包含具有两个列的嵌套表：$TIME，显示要预测的时间段；Quantity，包含预测的值。  
  
### <a name="example-2-adding-new-data-and-using-replace_model_cases"></a>示例 2：添加新数据和使用 REPLACE_MODEL_CASES  
 假定您发现某一特定地区的数据不正确，并且您希望使用模型中的模式，但是又想调整预测，以便与新数据匹配。 或者您可能发现另一地区的趋势更可靠，并且希望向不同地区中的数据应用最可靠的模型。  
  
 在这些方案中，您可以使用 REPLACE_MODEL_CASES 参数，并指定一组新的数据以用作历史数据。 这样，预测将基于指定模型中的模式，但将从新数据点末尾继续平滑地进行。 有关此方案的完整演练，请参阅[高级时序预测 &#40;中级数据挖掘教程&#41;](https://msdn.microsoft.com/library/b614ebdb-07ca-44af-a0ff-893364bd4b71)。  
  
 以下 PREDICTION JOIN 查询说明替换数据和进行新预测的语法。 对于替换数据，本示例检索 Amount 和 Quantity 列的值，并将每个值乘以 2：  
  
```  
SELECT [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 3, REPLACE_MODEL_CASES)   
FROM  
    [Forecasting]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT [ModelRegion],   
    ([Quantity] * 2) as Quantity,  
    ([Amount] * 2) as Amount,  
      [ReportingDate]  
    FROM [dbo].vTimeSeries  
    WHERE ModelRegion = N''M200 Pacific''  
    ') AS t  
ON  
  [Forecasting].[Model Region] = t.[ Model Region] AND  
[Forecasting].[Reporting Date] = t.[ReportingDate] AND  
[Forecasting].[Quantity] = t.[Quantity] AND  
[Forecasting].[Amount] = t.[Amount]  
```  
  
 下表比较了预测的结果。  
  
 原始预测：  
  
|Model Region|ReportingDate|数量|  
|-|-|-|  
|M200 Pacific|7/25/2008 12:00:00 AM|46|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|42|  
  
 更新的预测：  
  
|Model Region|ReportingDate|数量|  
|-|-|-|  
|M200 Pacific|7/25/2008 12:00:00 AM|91|  
|M200 Pacific|8/25/2008 12:00:00 AM|89|  
|M200 Pacific|9/25/2008 12:00:00 AM|84|  
  
### <a name="example-3-adding-new-data-and-using-extend_model_cases"></a>示例 3：添加新数据和使用 EXTEND_MODEL_CASES  
 示例3演示了如何使用*EXTEND_MODEL_CASES*选项来提供新数据，该数据将添加到现有数据序列的末尾。 新数据将添加到模型中，而不是替换现有数据点。  
  
 在下面的示例中，新数据是在 NATURAL PREDICTION JOIN 后的 SELECT 语句中提供的。 您可以使用此语法提供多个新输入行，但每个新输入行必须具有唯一的时间戳：  
  
```  
SELECT [Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 5, EXTEND_MODEL_CASES)   
FROM  
    [Forecasting]  
NATURAL PREDICTION JOIN  
    (SELECT  
        1 as [Reporting Date],  
        10 as [Quantity],  
        'M200 Europe' AS [Model Region]  
    UNION SELECT   
        2 as [Reporting Date],  
        15 as [Quantity],  
        'M200 Europe' AS [Model Region]  
) AS T  
WHERE ([Model Region] = 'M200 Europe'  
 OR [Model Region] = 'M200 Pacific')  
```  
  
 由于查询使用*EXTEND_MODEL_CASES*选项，因此 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会对其预测执行以下操作：  
  
-   向模型中添加两个月的新数据，从而增加了定型事例的总大小。  
  
-   在上一个事例数据的末尾启动预测。 因此，前两个预测表示刚添加到模型中的实际新销售数据。  
  
-   根据新扩展的模型返回其余三个时间段的新预测。  
  
 下表列出示例 2 查询的结果。 请注意，针对 M200 Europe 返回的前两个值与您提供的新值完全相同。 此行为是默认设置；如果您希望在新数据末尾启动预测，则必须指定开始和结束时间步长。 有关如何执行此操作的示例，请参阅[第5课：扩展时序模型](https://msdn.microsoft.com/library/7aad4946-c903-4e25-88b9-b087c20cb67d)。  
  
 另请注意，由于没有向太平洋地区提供新数据， 因此，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 返回所有（五个）时间段的新预测。  
  
 数量： M200 欧洲。 EXTEND_MODEL_CASES：  
  
|$TIME|数量|  
|-----------|--------------|  
|7/25/2008 0:00|10|  
|8/25/2008 0:00|15|  
|9/25/2008 0:00|72|  
|10/25/2008 0:00|69|  
|11/25/2008 0:00|68|  
  
 数量： M200 太平洋。 EXTEND_MODEL_CASES：  
  
|$TIME|数量|  
|-----------|--------------|  
|7/25/2008 0:00|46|  
|8/25/2008 0:00|44|  
|9/25/2008 0:00|42|  
|10/25/2008 0:00|42|  
|11/25/2008 0:00|38|  
  
## <a name="example-4-returning-statistics-in-a-time-series-prediction"></a>示例 4：返回时序预测中的统计信息  
 **PredictTimeSeries**函数不支持作为参数*INCLUDE_STATISTICS* 。 但是，可以使用以下查询来返回时序查询的预测统计信息。 此方法还可以与具有嵌套表列的模型结合使用。  
  
 在此特定模型中，可预测属性是数量，因此您必须使用 `[Quantity]` 作为 PredictTimeSeries 函数的第一个参数。 如果模型使用不同的可预测属性，则可以替换为不同的列名。  
  
```  
SELECT FLATTENED [Model Region],  
(SELECT   
     $Time,  
     [Quantity] as [PREDICTION],   
     PredictVariance([Quantity]) AS [VARIANCE],  
     PredictStdev([Quantity]) AS [STDEV]  
FROM  
      PredictTimeSeries([Quantity], 3) AS t  
) AS t  
FROM Forecasting  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 North America'  
```  
  
 示例结果：  
  
|Model Region|t.$TIME|t.PREDICTION|t.VARIANCE|t.STDEV|  
|------------------|-------------|------------------|----------------|-------------|  
|M200 Europe|7/25/2008 12:00:00 AM|121|11.6050581415597|3.40661975300439|  
|M200 Europe|8/25/2008 12:00:00 AM|142|10.678201866621|3.26775180615374|  
|M200 Europe|9/25/2008 12:00:00 AM|152|9.86897842568614|3.14149302493037|  
|M200 North America|7/25/2008 12:00:00 AM|163|1.20434529288162|1.20434529288162|  
|M200 North America|8/25/2008 12:00:00 AM|178|1.65031343900634|1.65031343900634|  
|M200 North America|9/25/2008 12:00:00 AM|156|1.68969399185442|1.68969399185442|  
  
> [!NOTE]  
>  在此示例中使用了 FLATTENED 关键字，目的是为了更好地在表中呈现结果；但是，如果提供程序支持分层行集，则可以省略 FLATTENED 关键字。 如果省略了 FLATTENED 关键字，则查询将返回两个列，第一列包含标识 `[Model Region]` 数据序列的值，第二列包含统计信息的嵌套表。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [时序模型查询示例](https://docs.microsoft.com/analysis-services/data-mining/time-series-model-query-examples)   
 [Predict (DMX)](../dmx/predict-dmx.md)  
  
  
