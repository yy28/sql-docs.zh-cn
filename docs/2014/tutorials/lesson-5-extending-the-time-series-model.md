---
title: 第 5 课： 扩展时序模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 7aad4946-c903-4e25-88b9-b087c20cb67d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7b67d295f79188cf83994225125886142c961e3b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48138220"
---
# <a name="lesson-5-extending-the-time-series-model"></a>第 5 课：扩展时序模型
  在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise 中，可以向时序模型中添加新数据，并自动将新数据合并到模型中。 您可以通过下列两种方式之一向时序挖掘模型添加新数据：  
  
-   使用 PREDICTION JOIN 将外部源中的数据联接到定型数据。  
  
-   使用单独预测查询每次向数据提供一个切片。  
  
 例如，假定您已经在几个月之前为现有销售数据的挖掘模型定型。 当您获得新的销售数据时，您可能希望更新销售预测以合并新数据。 这可以通过一个步骤来完成，即提供新销售数字作为输入数据并基于复合数据集生成新预测。  
  
## <a name="making-predictions-with-extendmodelcases"></a>使用 EXTEND_MODEL_CASES 进行预测  
 下面是几个使用 EXTEND_MODEL_CASES 进行时序预测的一般示例。 第一个示例使您能够从原始模型的最后一个时间步长开始指定预测数：  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>]  
```  
  
 第二个示例使您能够指定预测的起始时间步长和结束时间步长。 当您扩展模型事例时，此选项非常重要，这是因为在默认情况下用于预测查询的时间步长始终从原始序列的末尾开始。  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n-start, n-end, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>}  
```  
  
 在本教程中，您将创建两种查询。  
  
#### <a name="to-create-a-singleton-prediction-query-on-a-time-series-model"></a>针对时序模型创建单独预测查询  
  
1.  在中**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，依次指向**新查询**，然后单击**DMX**。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  将单独语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
    ```  
  
     使用：  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    ```  
  
     第一行从模型中检索用来标识序列的值。  
  
     第二行包含预测函数，该函数针对 Quantity 获得 6 个预测。 系统会向预测结果列分配一个别名 (`PredictQty`)，使结果更易于理解。  
  
4.  将  
  
    ```  
    FROM <mining model>  
    ```  
  
     使用：  
  
    ```  
    FROM [Forecasting_MIXED]  
    ```  
  
5.  将  
  
    ```  
    PREDICTION JOIN <source query>  
    ```  
  
     使用：  
  
    ```  
    NATURAL PREDICTION JOIN   
    (  
       SELECT 1 AS [Reporting Date],  
       '10' AS [Quantity],  
       'M200 Europe' AS [Model Region]  
       UNION SELECT  
       2 AS [Reporting Date],  
       15 AS [Quantity]),  
       'M200 Europe' AS [Model Region]  
    ) AS t  
    ```  
  
6.  将  
  
    ```  
    [WHERE <criteria>]  
    ```  
  
     使用：  
  
    ```  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    FROM  
       [Forecasting_MIXED]  
    NATURAL PREDICTION JOIN   
       SELECT 1 AS [ReportingDate],  
      '10' AS [Quantity],  
      'M200 Europe' AS [ModelRegion]  
    UNION SELECT  
      2 AS [ReportingDate],  
      15 AS [Quantity]),  
      'M200 Europe' AS [ModelRegion]  
    ) AS t  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
7.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
8.  在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`Singleton_TimeSeries_Query.dmx`。  
  
9. 在工具栏上，单击**Execute**按钮。  
  
     该查询将返回 Europe 和 Pacific 地区 M200 自行车的销售量预测。  
  
## <a name="understanding-prediction-start-with-extendmodelcases"></a>了解以 EXTEND_MODEL_CASES 开始的预测  
 现在，您已经基于原始模型用新数据创建了预测，现在可以对结果进行比较，以了解销售数据更新对预测的影响。 在这样做之前，请检查刚创建的代码，并注意以下事项：  
  
-   您仅为 Europe 地区提供了新数据。  
  
-   您只提供了两个月的新数据。  
  
 下表显示了为 M200 Europe 提供的新值对预测的影响。 您没有为 Pacific 地区的 M200 产品提供任何新数据，只是为了进行比较而提供此序列：  
  
 **产品和区域： M200 Europe**  
  
|||||  
|-|-|-|-|  
|||现有模型 (`PredictTimeSeries`)|具有更新销售数据的模型（具有 `PredictTimeSeries` 的 `EXTEND_MODEL_CASES`）|  
|M200 Europe|7/25/2008 12:00:00 AM|77|10|  
|M200 Europe|8/25/2008 12:00:00 AM|64|15|  
|M200 Europe|9/25/2008 12:00:00 AM|59|72|  
|M200 Europe|10/25/2008 12:00:00 AM|56|69|  
|M200 Europe|11/25/2008 12:00:00 AM|56|68|  
|M200 Europe|12/25/2008 12:00:00 AM|74|89|  
  
 **产品和区域： M200 Pacific**  
  
|||||  
|-|-|-|-|  
|||现有模型 (`PredictTimeSeries`)|具有更新销售数据的模型（具有 `PredictTimeSeries` 的 `EXTEND_MODEL_CASES`）|  
|M200 Pacific|7/25/2008 12:00:00 AM|41|41|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|38|38|  
|M200 Pacific|10/25/2008 12:00:00 AM|41|41|  
|M200 Pacific|11/25/2008 12:00:00 AM|36|36|  
|M200 Pacific|12/25/2008 12:00:00 AM|39|39|  
  
 从这些结果中，可以得出以下两个结论：  
  
-   M200 Europe 序列的前两个预测与您提供的新数据完全相同。 在设计上，Analysis Services 返回实际的新数据点，而不进行预测。 这是因为您扩展模型事例时，用于预测查询的时间步长始终从原始序列的末尾开始。 因此，如果添加两个新数据点，返回的前两个预测将会与新数据重叠。  
  
-   用完所有新数据点之后，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将基于更新后的模型进行预测。 因此，可以看出，从 2004 年 9 月份开始，基于原始模型的 M200 Europe 预测（位于左列）和基于使用 EXTEND_MODEL_CASES 的模型的 M200 Europe 预测（位于右侧）之间的区别。 由于模型用新数据进行了更新，因此预测有所不同。  
  
## <a name="using-start-and-end-time-steps-to-control-predictions"></a>使用开始时间步长和结束时间步长控制预测  
 扩展模型时，新数据始终附加到序列的末尾。 但是，为了进行预测，用于预测查询的时间段始终从原始序列的末尾开始。 如果您只想在添加新数据时获得新预测，则必须将起始点指定为许多时间段。 例如，如果要添加两个新数据点并希望进行四个新预测，您需要执行下列操作：  
  
-   针对时序模型创建一个 PREDICTION JOIN，然后指定两个月的新数据。  
  
-   请求对四个时间段进行预测，其中起点是时间片 3，终点是时间片 6。  
  
 换而言之，如果您的新数据包含 n 个时间段，并请求对时间步长 1 至 n，则预测将与新数据的时间段一致。 若要获取对数据未覆盖的时间段的新预测，您必须从新数据序列之后的时间段 n+1 处开始预测，或者确保您请求了其他的时间段。  
  
> [!NOTE]  
>  添加新数据时不能进行历史预测。  
  
 下面的示例显示了一条 DMX 语句，使用该语句可仅获得对上例中两个序列的新预测。  
  
```  
SELECT [Model Region],  
PredictTimeSeries([Quantity],3,6, EXTEND_MODEL_CASES) AS PredictQty  
FROM  
   [Forecasting_MIXED]  
NATURAL PREDICTION JOIN   
   SELECT 1 AS [ReportingDate],  
  '10' AS [Quantity],  
  'M200 Europe' AS [ModelRegion]  
UNION SELECT  
  2 AS [ReportingDate],  
  15 AS [Quantity]),  
  'M200 Europe' AS [ModelRegion]  
) AS t  
WHERE [ModelRegion] = 'M200 Europe'  
```  
  
 预测结果从时间段 3 开始，该时间段在您提供的 2 个月的新数据之后。  
  
 **产品和区域： M200 Europe**  
  
 具有更新数据的模型（具有 EXTEND_MODEL_CASES 的 PredictTimeSeries）  
  
||||  
|-|-|-|  
|M200 Europe|9/25/2008 12:00:00 AM|72|  
|M200 Europe|10/25/2008 12:00:00 AM|69|  
|M200 Europe|11/25/2008 12:00:00 AM|68|  
|M200 Europe|12/25/2008 12:00:00 AM|89|  
  
## <a name="making-predictions-with-replacemodelcases"></a>使用 REPLACE_MODEL_CASES 进行预测  
 如果您想对一组事例的某个模型定型，然后将该模型应用到不同的数据序列，则替换模型事例非常有用。 此方案的详细的演练所示[第 2 课： 生成预测方案&#40;数据挖掘中级教程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)。  
  
## <a name="see-also"></a>请参阅  
 [时序模型查询示例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
