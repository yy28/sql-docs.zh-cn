---
title: 第 3 课：处理时序结构和模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 16e27b57-eae1-47a7-a02c-47b6ed487d87
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 493d27c9836eb765c655eba5bbb004e4d48cde40
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042873"
---
# <a name="lesson-3-processing-the-time-series-structure-and-models"></a>第 3 课：处理时序结构和模型
  在本课程中，您将使用[INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx)语句处理挖掘结构和挖掘模型创建的时序。  
  
 处理挖掘结构时，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将读取源数据并生成支持挖掘模型的结构。 您必须始终在首次创建挖掘模型和结构时对它进行处理。 如果使用 INSERT INTO 指定挖掘结构，该语句将处理挖掘结构及其关联的所有挖掘模型。  
  
 如果将挖掘模型添加到已处理过的挖掘结构中，则可以利用 `INSERT INTO MINING MODEL` 语句使用现有数据只处理新挖掘模型。  
  
 有关处理挖掘模型的详细信息，请参阅[处理要求和注意事项&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
## <a name="insert-into-statement"></a>INSERT INTO 语句  
 为了定型时序挖掘结构及其所有关联的挖掘模型，请使用[INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx)语句。 可以将该语句中的代码分为下列几部分。  
  
-   标识挖掘结构  
  
-   列出挖掘结构中的列  
  
-   定义定型数据  
  
 下面是 `INSERT INTO` 语句的一般示例：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
)  
OPENQUERY (<source data definition>)  
```  
  
 代码的第一行标识将定型的挖掘结构：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 代码的接下来各行指定该挖掘结构定义的列。 必须列出挖掘结构的每一列，并且每列必须映射到源查询数据所包含的对应列。  
  
```  
(  
   <mining structure columns>  
)  
```  
  
 代码的最后几行定义将用于定型挖掘结构的数据。  
  
```  
OPENQUERY (<source data definition>)  
```  
  
 在本课中，您将使用 `OPENQUERY` 来定义源数据。 有关针对源数据定义查询的其他方法的详细信息，请参阅[&#60;源数据查询&#62;](/sql/dmx/source-data-query)。  
  
## <a name="lesson-tasks"></a>课程任务  
 在本课程中，将执行以下任务：  
  
-   处理挖掘结构 Forecasting_MIXED_Structure  
  
-   处理相关的挖掘模型 Forecasting_MIXED、Forecasting_ARIMA 和 Forecasting_ARTXP  
  
## <a name="processing-the-time-series-mining-structure"></a>处理时序挖掘结构  
  
#### <a name="to-process-the-mining-structure-and-related-mining-models-by-using-insert-into"></a>使用 INSERT INTO 处理挖掘结构和相关的挖掘模型  
  
1.  在中**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，依次指向**新查询**，然后单击**DMX**。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  将 INSERT INTO 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    [<mining structure>]  
    ```  
  
     使用：  
  
    ```  
    Forecasting_MIXED_Structure  
    ```  
  
4.  将  
  
    ```  
    <mining structure columns>  
    ```  
  
     使用：  
  
    ```  
    [ReportingDate],  
    [ModelRegion]   
    ```  
  
5.  将  
  
    ```  
    OPENQUERY(<source data definition>)  
    ```  
  
     使用：  
  
    ```  
    OPENQUERY([Adventure Works DW 2008R2],'SELECT [ReportingDate], [ModelRegion], [Quantity], [Amount]  
    FROM vTimeSeries ORDER BY [ReportingDate]')  
    ```  
  
     源查询引用[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]中级教程示例项目中定义的数据源。 它使用此数据源来访问视图 vTimeSeries。 此视图包含将用于定型挖掘模型的源数据。 如果您不熟悉此项目或此视图，请参阅[第 2 课：生成预测方案&#40;数据挖掘中级教程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)。  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    INSERT INTO MINING STRUCTURE [Forecasting_MIXED_Structure]  
    (  
       [ReportingDate],[ModelRegion],[Quantity],[Amount])  
    )  
    OPENQUERY(  
    [Adventure Works DW 2008R2],  
    'SELECT [ReportingDate],[ModelRegion],[Quantity],[Amount] FROM vTimeSeries ORDER BY [ReportingDate]'  
    )   
    ```  
  
6.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
7.  在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`ProcessForecastingAll.dmx`。  
  
8.  在工具栏上，单击**Execute**按钮。  
  
 在该查询完成运行之后，可以使用处理过的挖掘模型创建预测。 在下一课中，您将基于创建的挖掘模型创建多个预测。  
  
## <a name="next-lesson"></a>下一课  
 [第 4 课：创建时序预测使用 DMX](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
  
## <a name="see-also"></a>请参阅  
 [处理要求和注意事项&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)   
 [&#60;源数据查询&#62;](/sql/dmx/source-data-query)   
 [OPENQUERY &AMP;#40;DMX&AMP;#41;](/sql/dmx/source-data-query-openquery)  
  
  
