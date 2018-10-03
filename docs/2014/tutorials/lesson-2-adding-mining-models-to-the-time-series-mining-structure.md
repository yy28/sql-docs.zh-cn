---
title: 第 2 课： 向时序挖掘结构添加挖掘模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 75c2a74b-21ce-44fb-a26b-68be4c685c12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8efde3304c2aa0ff51936754e6cba255d3dce4de
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158427"
---
# <a name="lesson-2-adding-mining-models-to-the-time-series-mining-structure"></a>第 2 课：向时序挖掘结构添加挖掘模型
  在本课中，将新的挖掘模型添加到刚刚创建的挖掘结构[第 1 课： 创建时序挖掘模型和挖掘结构](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)。  
  
## <a name="alter-mining-structure-statement"></a>ALTER MINING STRUCTURE 语句  
 为了向现有挖掘结构添加新的挖掘模型，可以使用 [ALTER MINING STRUCTURE &#40;DMX&#41;] （(~/dmx/alter-mining-structure-dmx.md) 语句。 可以将语句中的代码分为下列几部分：  
  
-   标识挖掘结构  
  
-   命名挖掘模型  
  
-   定义键列  
  
-   定义可预测列  
  
-   指定算法和任何参数更改  
  
 下面是 ALTER MINING STRUCTURE 语句的一般示例：  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
ADD MINING MODEL [<mining model name>]  
   ([<key columns>],  
    <mining model columns>  
   )  
USING <algorithm name>([<algorithm parameters>])  
[WITH DRILLTHROUGH]  
```  
  
 代码的第一行标识将向其添加挖掘模型的现有挖掘结构：  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 代码的第二行对将要添加到挖掘结构中的挖掘模型进行命名：  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 有关命名 DMX 中的对象的信息，请参阅[标识符&#40;DMX&#41;](/sql/dmx/identifiers-dmx)。  
  
 代码的接下来的各行定义挖掘结构中将由挖掘模型使用的各列：  
  
```  
[<key columns>],  
<mining model columns>  
```  
  
 您只能使用挖掘结构中现有的各列，列表中的第一列必须是挖掘结构中的键列。  
  
 代码的下一行定义生成挖掘模型的挖掘算法以及可以针对算法设置的算法参数，并指定是否能够从挖掘模型深化到定型事例中的详细数据视图：  
  
```  
USING <algorithm name>([<algorithm parameters>])  
WITH DRILLTHROUGH  
```  
  
 您可以调整的算法参数的详细信息，请参阅[Microsoft Time Series Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)。  
  
 您可以使用以下语法指定将挖掘模型中的一列用于预测：  
  
```  
<mining model column> PREDICT  
```  
  
## <a name="lesson-tasks"></a>课程任务  
 在本课程中，将执行以下任务：  
  
-   在结构中添加新的时序挖掘模型。  
  
-   更改算法参数以使用另一种分析和预测方法。  
  
## <a name="adding-an-arima-time-series-model-to-the-structure"></a>在结构中添加 ARIMA 时序模型  
 第一步是在现有结构中添加新的预测挖掘模型。 默认情况下，[!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法通过使用 ARIMA 和 ARTXP 两种算法并混合所得到的结果来创建时序挖掘模型。 但是，您可以指定要使用某个算法，也可以指定确切的算法组合。 在该步骤中，您将添加一个仅使用 ARIMA 算法的新模型。 该算法针对长期预测进行了优化。  
  
#### <a name="to-add-an-arima-time-series-mining-model"></a>添加 ARIMA 时序挖掘模型  
  
1.  在**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，依次指向**新查询**，然后单击**DMX**若要打开查询编辑器和一个新的空白查询。  
  
2.  将 ALTER MINING STRUCTURE 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    <mining structure name>   
    ```  
  
     使用：  
  
    ```  
    [Forecasting_MIXED_Structure]  
    ```  
  
4.  将  
  
    ```  
    <mining model name>   
    ```  
  
     使用：  
  
    ```  
    Forecasting_ARIMA  
    ```  
  
5.  将  
  
    ```  
    <key columns>,  
    ```  
  
     使用：  
  
    ```  
    [ReportingDate],  
    [ModelRegion]  
    ```  
  
     请注意，您不必重复在 CREATE MINING MODEL 语句中提供的有关数据类型或内容类型的任何信息，因为这些信息已经存储在挖掘结构中。  
  
6.  将  
  
    ```  
    <mining model columns>  
    ```  
  
     使用：  
  
    ```  
    ([Quantity] PREDICT,  
    [Amount] PREDICT  
    )  
    ```  
  
7.  将  
  
    ```  
    USING <algorithm name>([<algorithm parameters>])   
    [WITH DRILLTHROUGH]  
    ```  
  
     使用：  
  
    ```  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
     现在，结果语句应该如下所示：  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARIMA]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
8.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
9. 在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`Forecasting_ARIMA.dmx`。  
  
10. 在工具栏上，单击**Execute**按钮。  
  
## <a name="adding-an-artxp-time-series-model-to-the-structure"></a>在结构中添加 ARTXP 时序模型  
 ARTXP 算法是 SQL Server 2005 中的默认时序算法，针对短期预测进行了优化。 若要使用所有这三个时序算法来比较预测结果，还需要再添加一个基于 ARTXP 算法的模型。  
  
#### <a name="to-add-an-artxp-time-series-mining-model"></a>添加 ARTXP 时序挖掘模型  
  
1.  将以下代码复制到空白的查询窗口中。  
  
     请注意，除了新挖掘模型的名称以及 FORECAST_METHOD 参数的值，您不必更改任何其他内容。  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARTXP]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARTXP')  
    WITH DRILLTHROUGH  
    ```  
  
2.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
3.  在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`Forecasting_ARTXP.dmx`。  
  
4.  在工具栏上，单击**Execute**按钮。  
  
 在下一课中，您将处理所有模型和挖掘结构。  
  
## <a name="next-lesson"></a>下一课  
 [第 3 课：准备时序结构和模型](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 时序算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Microsoft 时序算法技术参考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
