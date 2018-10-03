---
title: 第 4 课： 执行市场篮预测 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b3238f1b-ea04-4253-ade2-838a806b62fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6db486a5d497ba6b6c5bfe312197d78a5656d388
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177487"
---
# <a name="lesson-4-executing-market-basket-predictions"></a>第 4 课：执行市场篮预测
  在本课程中，您将使用 DMX`SELECT`语句以创建基于关联的预测模型中创建[第 2 课： 向市场篮挖掘结构添加挖掘模型](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)。 使用 DMX `SELECT` 语句并添加一个 `PREDICTION JOIN` 子句可创建一个预测查询。 预测联接语法的详细信息，请参阅[SELECT FROM&#60;模型&#62;预测联接&#40;DMX&#41;](/sql/dmx/select-from-model-cases-dmx)。  
  
 **SELECT FROM\<模型 > PREDICTION JOIN**形式的`SELECT`语句包含三个部分：  
  
-   结果集中返回的挖掘模型列和预测函数的列表。 此列表还可以包含源数据中的输入列。  
  
-   定义用于创建预测的数据的源查询。 例如，如果您正批量创建多个预测，则源查询可以检索客户列表。  
  
-   挖掘模型列和源数据之间的映射。 如果列名称匹配，则可以使用 `NATURAL PREDICTION JOIN` 语法并忽略列映射。  
  
 使用预测函数可增强查询。 预测功能提供其他信息，例如，预测出现的概率或对定性数据集中预测的支持。 有关预测函数的详细信息，请参阅[函数&#40;DMX&#41;](/sql/dmx/functions-dmx)。  
  
 您还可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的预测查询生成器创建预测查询。  
  
## <a name="singleton-prediction-join-statement"></a>单独 PREDICTION JOIN 语句  
 第一步是创建单独查询，通过使用**SELECT FROM\<模型 > PREDICTION JOIN**语法和提供一组的值作为输入。 下面是单独语句的一般示例：  
  
```  
SELECT <select list>  
    FROM [<mining model>]   
[NATURAL] PREDICTION JOIN  
(SELECT '<value>' AS [<column>],   
    (SELECT 'value' AS [<nested column>] UNION  
        SELECT 'value' AS [<nested column>] ...)   
    AS [<nested table>])  
AS [<input alias>]  
```  
  
 代码的第一行定义查询返回的挖掘模型中的列，并指定用于生成预测的挖掘模型的名称：  
  
```  
SELECT <select list> FROM [<mining model>]   
```  
  
 代码的下一行指示要执行的操作。 因为要指定每个列的值并准确键入列名称以便与模型匹配，所以可以使用 `NATURAL PREDICTION JOIN` 语法。 但是，如果列名不同，您将必须通过添加 `ON` 子句来指定模型中的列与新数据中的列之间的映射。  
  
```  
[NATURAL] PREDICTION JOIN  
```  
  
 代码的以下各行定义购物车中将用于预测客户将添加的其他产品的产品：  
  
```  
(SELECT '<value>' AS [<column>],   
    (SELECT 'value' AS [<nested column>] UNION  
        SELECT 'value' AS [<nested column>] ...)   
    AS [<nested table>])  
```  
  
## <a name="lesson-tasks"></a>课程任务  
 在本课程中，将执行以下任务：  
  
-   根据在其购物车中的已有项创建一个查询，预测客户可能购买，哪些其他项。 您将使用默认使用挖掘模型创建此查询*MINIMUM_PROBABILITY*。  
  
-   根据客户购物车中的已有项创建一个查询，预测客户可能购买的其他项。 此查询基于不同的模型，在其中*MINIMUM_PROBABILITY*已设置为 0.01。 因为的默认值为*MINIMUM_PROBABILITY*关联模型中为 0.3，此模型中的查询应返回与对默认模型相比，该查询更可能的项。  
  
## <a name="create-a-prediction-by-using-a-model-with-the-default-minimumprobability"></a>使用带有默认 MINIMUM_PROBABILITY 的模型创建预测  
  
#### <a name="to-create-an-association-query"></a>创建关联查询  
  
1.  在**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，依次指向**新查询**，然后单击**DMX**以打开查询编辑器。  
  
2.  将 `PREDICTION JOIN` 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    <select list>   
    ```  
  
     使用：  
  
    ```  
    PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
     您可以只包括列名 [Products]，但通过使用[Predict &#40;DMX&#41; ](/sql/dmx/predict-dmx)函数，可以限制为三种由算法返回的产品数量。 还可以使用 `INCLUDE_STATISTICS`，它将返回每种产品的支持、概率以及校正后的概率。 这些统计信息有助于您对预测的准确性进行分级。  
  
4.  将  
  
    ```  
    [<mining model>]   
    ```  
  
     使用：  
  
    ```  
    [Default Association]  
    ```  
  
5.  将  
  
    ```  
    (SELECT '<value>' AS [<column>],   
        (SELECT 'value' AS [<nested column>] UNION  
            SELECT 'value' AS [<nested column>] ...)   
        AS [<nested table>])  
    ```  
  
     使用：  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     此语句使用 `UNION` 语句来指定三种产品，这三种产品必须与预测的产品一起包含在购物车中。 `SELECT` 语句中的 Model 列对应于嵌套产品表中所包含的模型列。  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    SELECT  
      PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    From  
      [Default Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
6.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
7.  在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`Association Prediction.dmx`。  
  
8.  在工具栏上，单击**Execute**按钮。  
  
     查询将返回包含以下三种产品的表：HL Mountain Tire、Fender Set – Mountain 和 ML Mountain Tire。 该表按概率顺序列出这些返回的产品。 最有可能包含在查询指定的三种产品所在购物车中的返回的产品将出现在表的顶部。 其次最有可能包含在购物车中的产品是下面的两种产品。 该表还包含说明预测准确性的统计信息。  
  
## <a name="create-a-prediction-by-using-a-model-with-a-minimumprobability-of-001"></a>使用 MINIMUM_PROBABILITY 为 0.01 的模型创建预测  
  
#### <a name="to-create-an-association-query"></a>创建关联查询  
  
1.  在**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，依次指向**新查询**，然后单击**DMX**以打开查询编辑器。  
  
2.  将 `PREDICTION JOIN` 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    <select list>   
    ```  
  
     使用：  
  
    ```  
    PREDICT([Modified Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
4.  将  
  
    ```  
    [<mining model>]   
    ```  
  
     使用：  
  
    ```  
    [Modified Association]  
    ```  
  
5.  将  
  
    ```  
    (SELECT '<value>' AS [<column>],   
        (SELECT 'value' AS [<nested column>] UNION  
            SELECT 'value' AS [<nested column>] ...)   
        AS [<nested table>])  
    ```  
  
     使用：  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     此语句使用 `UNION` 语句来指定三种产品，这三种产品必须与预测的产品一起包含在购物车中。 `SELECT` 语句中的 `[Model]` 列对应于嵌套产品表中的列。  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    SELECT  
      PREDICT([Modified Association].[Products],INCLUDE_STATISTICS,3)  
    From  
      [Modified Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
6.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
7.  在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`Modified Association Prediction.dmx`。  
  
8.  在工具栏上，单击**Execute**按钮。  
  
     查询将返回包含以下三种产品的表：HL Mountain Tire、Water Bottle 和 Fender Set - Mountain。 该表按概率顺序列出这些产品。 出现在该表顶部的产品是最有可能包含在查询指定的三种产品所在购物车中的产品。 其余产品是其次最有可能包含在该购物车中的产品。 该表还包含描述的预测准确性的统计信息。  
  
     您可以看到从查询的此结果的值*MINIMUM_PROBABILITY*参数会影响由查询返回的结果。  
  
 这是市场篮教程中的最后一个步骤。 您现在即可拥有一组模型，并可通过该组模型预测客户可能同时购买的产品。  
  
 若要了解如何使用 DMX 中其他预测情况下，请参阅[自行车购买者 DMX 教程](../../2014/tutorials/bike-buyer-dmx-tutorial.md)。  
  
## <a name="see-also"></a>请参阅  
 [关联模型查询示例](../../2014/analysis-services/data-mining/association-model-query-examples.md)   
 [数据挖掘查询接口](../../2014/analysis-services/data-mining/data-mining-query-tools.md)  
  
  
