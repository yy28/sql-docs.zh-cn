---
title: 第3课：处理时序结构和模型 |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63042873"
---
# <a name="lesson-3-processing-the-time-series-structure-and-models"></a>第 3 课：准备时序结构和模型
  在本课中，您将使用[INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx)语句来处理所创建的时序挖掘结构和挖掘模型。  
  
 处理挖掘结构时，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将读取源数据并生成支持挖掘模型的结构。 您必须始终在首次创建挖掘模型和结构时对它进行处理。 如果使用 INSERT INTO 指定挖掘结构，该语句将处理挖掘结构及其关联的所有挖掘模型。  
  
 如果将挖掘模型添加到已处理过的挖掘结构中，则可以利用 `INSERT INTO MINING MODEL` 语句使用现有数据只处理新挖掘模型。  
  
 有关处理挖掘模型的详细信息，请参阅[处理 &#40;数据挖掘&#41;的要求和注意事项](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
## <a name="insert-into-statement"></a>INSERT INTO 语句  
 为了训练时序挖掘结构及其所有关联的挖掘模型，请使用[INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx)语句。 可以将该语句中的代码分为下列几部分。  
  
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
  
 在本课中，您将使用 `OPENQUERY` 来定义源数据。 有关为源数据定义查询的其他方法的详细信息，请参阅[&#60;源数据查询&#62;](/sql/dmx/source-data-query)。  
  
## <a name="lesson-tasks"></a>课程任务  
 您将在本课中执行以下任务：  
  
-   处理挖掘结构 Forecasting_MIXED_Structure  
  
-   处理相关的挖掘模型 Forecasting_MIXED、Forecasting_ARIMA 和 Forecasting_ARTXP  
  
## <a name="processing-the-time-series-mining-structure"></a>处理时序挖掘结构  
  
#### <a name="to-process-the-mining-structure-and-related-mining-models-by-using-insert-into"></a>使用 INSERT INTO 处理挖掘结构和相关的挖掘模型  
  
1.  在**对象资源管理器**中，右键单击实例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向 "**新建查询**"，然后单击 " **DMX**"。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  将 INSERT INTO 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    [<mining structure>]  
    ```  
  
     替换为：  
  
    ```  
    Forecasting_MIXED_Structure  
    ```  
  
4.  将  
  
    ```  
    <mining structure columns>  
    ```  
  
     替换为：  
  
    ```  
    [ReportingDate],  
    [ModelRegion]   
    ```  
  
5.  将  
  
    ```  
    OPENQUERY(<source data definition>)  
    ```  
  
     替换为：  
  
    ```  
    OPENQUERY([Adventure Works DW 2008R2],'SELECT [ReportingDate], [ModelRegion], [Quantity], [Amount]  
    FROM vTimeSeries ORDER BY [ReportingDate]')  
    ```  
  
     源查询引用在中级教程[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]示例项目中定义的数据源。 它使用此数据源来访问视图 vTimeSeries。 此视图包含将用于定型挖掘模型的源数据。 如果你不熟悉此项目或此视图，请参阅[第2课：生成预测方案 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)。  
  
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
  
6.  在 "**文件**" 菜单上，单击 "**将 DMXQuery1 另存为**"。  
  
7.  在 "**另存为**" 对话框中，浏览到相应的文件夹，并将`ProcessForecastingAll.dmx`该文件命名为。  
  
8.  在工具栏上，单击 "**执行**" 按钮。  
  
 在该查询完成运行之后，可以使用处理过的挖掘模型创建预测。 在下一课中，您将基于创建的挖掘模型创建多个预测。  
  
## <a name="next-lesson"></a>下一课  
 [第 4 课：使用 DMX 创建时序预测](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘 &#40;处理要求和注意事项&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)   
 [&#60;源数据查询&#62;](/sql/dmx/source-data-query)   
 [OPENQUERY &#40;DMX&#41;](/sql/dmx/source-data-query-openquery)  
  
  
