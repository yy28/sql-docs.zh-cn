---
title: 第 1 课：创建时序挖掘模型和挖掘结构 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b201f2b8-9ab5-425b-9ff3-fe321a60a7b7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2513bc3837dd224f6561eb0015ced538ea3add8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678453"
---
# <a name="lesson-1-creating-a-time-series-mining-model-and-mining-structure"></a>第 1 课：创建时序挖掘模型和挖掘结构
  在本课中，将创建一个挖掘模型，可以使用该模型根据历史数据预测一段时间内的值。 创建该模型时，基础结构会自动生成，且可以用作其他挖掘模型的基础。  
  
 本课假定您已熟悉预测模型以及 Microsoft 时序算法的要求。 有关详细信息，请参阅 [Microsoft Time Series Algorithm](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)。  
  
## <a name="create-mining-model-statement"></a>创建挖掘模型语句  
 若要直接创建挖掘模型并自动生成基础挖掘结构，则使用[CREATE MINING MODEL &#40;DMX&#41; ](/sql/dmx/create-mining-model-dmx)语句。 可以将语句中的代码分为下列几部分：  
  
-   命名模型  
  
-   定义时间戳  
  
-   定义可选序列键列  
  
-   定义可预测属性  
  
 下面是 CREATE MINING MODEL 语句的一般示例：  
  
```  
CREATE MINING MODEL [<Mining Structure Name>]  
(  
   <key columns>,  
   <predictable attribute columns>  
)  
USING <algorithm name>([parameter list])  
WITH DRILLTHROUGH  
```  
  
 代码的第一行定义了挖掘模型的名称：  
  
```  
CREATE MINING MODEL [Mining Model Name]  
```  
  
 通过在模型名称后追加“_structure”，Analysis Services 自动生成基础结构的名称，这样可以确保将结构名称与模型名称区分开。 有关命名 DMX 中的对象的信息，请参阅[标识符&#40;DMX&#41;](/sql/dmx/identifiers-dmx)。  
  
 代码中的下一行定义了挖掘模型的键列，如果是时序模型，则它可唯一标识源数据中的时间步长。 时间步长在列名和数据类型后使用 `KEY TIME` 关键字进行标识。 如果时序模型具有单独的序列键，则使用 `KEY` 关键字对它进行标识。  
  
```  
<key columns>  
```  
  
 代码中的下一行用于定义将预测的模型中的列。 一个挖掘模型中可以有多个可预测属性。 如果有多个可预测属性，Microsoft 时序算法会为每个序列生成一个单独的分析：  
  
```  
<predictable attribute columns>  
```  
  
## <a name="lesson-tasks"></a>课程任务  
 在本课程中，将执行以下任务：  
  
-   创建新的空白查询  
  
-   更改查询以创建挖掘模型  
  
-   执行查询  
  
## <a name="creating-the-query"></a>创建查询  
 第一步是连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例，并在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中创建一个新的 DMX 查询。  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中创建一个新的 DMX 查询  
  
1.  打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  在中**连接到服务器**对话框中，对于**服务器类型**，选择**Analysis Services**。 在中**服务器名称**，类型`LocalHost`，或实例的名称[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]想要连接到本课程中。 单击 **“连接”**。  
  
3.  在中**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，依次指向**新查询**，然后单击**DMX**。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
## <a name="altering-the-query"></a>更改查询  
 下一步是修改 CREATE MINING MODEL 语句，以创建用于预测的挖掘模型及其基础挖掘结构。  
  
#### <a name="to-customize-the-create-mining-model-statement"></a>自定义 CREATE MINING MODEL 语句  
  
1.  在查询编辑器中，将 CREATE MINING MODEL 语句的一般示例复制到空白查询中。  
  
2.  将  
  
    ```  
    [mining model name]   
    ```  
  
     使用：  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
3.  将  
  
    ```  
    <key columns>  
    ```  
  
     使用：  
  
    ```  
    [Reporting Date] DATE KEY TIME,  
    [Model Region] TEXT KEY  
    ```  
  
     `TIME KEY` 关键字指示 ReportingDate 列包含用于对值进行排序的时间步长值。 时间步长可以为日期和时间、整数或任何有序数据类型，只要值唯一且数据有序即可。  
  
     `TEXT` 和 `KEY` 关键字指示 ModelRegion 列包含额外的序列键。 只能有一个序列键，并且该列中的值必须是唯一的。  
  
4.  将  
  
    ```  
    < predictable attribute columns> )  
    ```  
  
     使用：  
  
    ```  
    [Quantity] LONG CONTINUOUS PREDICT,  
    [Amount] DOUBLE CONTINUOUS PREDICT  
    )  
    ```  
  
5.  将  
  
    ```  
    USING <algorithm name>([parameter list])  
    WITH DRILLTHROUGH  
    ```  
  
     使用：  
  
    ```  
    USING Microsoft_Time_Series(AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
    ```  
  
     算法参数 `AUTO_DETECT_PERIODICITY` = 0.8 指示您希望使用该算法来检测数据中的周期。 如果将此值设置为接近于 1 的数，往往会发现许多模式，不过会降低处理速度。  
  
     算法参数 `FORECAST_METHOD` 指示您是否希望使用 ARTXP、ARIMA 或两者的组合来对数据进行分析。  
  
     关键字 `WITH DRILLTHROUGH` 指示您希望能够在模型完成后查看源数据中的详细统计信息。 如果希望使用 Microsoft 时序查看器浏览模型，则必须添加此子句。 它不是预测所必需的。  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    CREATE MINING MODEL [Forecasting_MIXED]  
         (  
        [Reporting Date] DATE KEY TIME,  
        [Model Region] TEXT KEY,  
        [Quantity] LONG CONTINUOUS PREDICT,  
        [Amount] DOUBLE CONTINUOUS PREDICT  
        )  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
  
    ```  
  
6.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
7.  在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`Forecasting_MIXED.dmx`。  
  
## <a name="executing-the-query"></a>执行查询  
 最后一步是执行查询。 创建并保存查询后，需要执行查询，以在服务器上创建挖掘模型及其挖掘结构。 有关在查询编辑器中执行查询的详细信息，请参阅[数据库引擎查询编辑器&#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)。  
  
#### <a name="to-execute-the-query"></a>若要执行查询  
  
-   在查询编辑器中，在工具栏上，单击**Execute**。  
  
     查询的状态显示在**消息**在底部的查询编辑器执行完语句后的选项卡。 所显示的消息应为：  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     名为的新结构**Forecasting_MIXED_Structure**服务器，以及相关的挖掘模型上现在存在**Forecasting_MIXED**。  
  
 在下一课中，您将添加到挖掘模型**Forecasting_MIXED**刚创建的挖掘结构。  
  
## <a name="next-lesson"></a>下一课  
 [第 2 课：向时序挖掘结构添加挖掘模型](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
  
## <a name="see-also"></a>请参阅  
 [时序模型的挖掘模型内容&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)   
 [Microsoft 时序算法技术参考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
