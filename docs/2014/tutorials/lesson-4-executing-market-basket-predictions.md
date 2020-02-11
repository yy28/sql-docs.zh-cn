---
title: 第4课：执行市场篮预测 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b3238f1b-ea04-4253-ade2-838a806b62fe
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3b49fc242eb8b2242269c5af33cc094937bbe0de
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63312112"
---
# <a name="lesson-4-executing-market-basket-predictions"></a>第 4 课：执行市场篮预测
  在本课中，您将使用 DMX `SELECT`语句根据您在[第2课：向市场篮挖掘结构中添加挖掘模型](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)中创建的关联模型创建预测。 使用 DMX `SELECT` 语句并添加一个 `PREDICTION JOIN` 子句可创建一个预测查询。 有关预测联接的语法的详细信息，请参阅[&#60;模型中选择&#62; 预测联接 &#40;DMX&#41;](/sql/dmx/select-from-model-cases-dmx)。  
  
 语句 **> 预测\<联接窗体的 SELECT FROM 模型**包含三个部分： `SELECT`  
  
-   结果集中返回的挖掘模型列和预测函数的列表。 此列表还可以包含源数据中的输入列。  
  
-   定义用于创建预测的数据的源查询。 例如，如果您正批量创建多个预测，则源查询可以检索客户列表。  
  
-   挖掘模型列和源数据之间的映射。 如果列名称匹配，则可以使用 `NATURAL PREDICTION JOIN` 语法并忽略列映射。  
  
 使用预测函数可增强查询。 预测功能提供其他信息，例如，预测出现的概率或对定性数据集中预测的支持。 有关预测函数的详细信息，请参阅[函数 &#40;DMX&#41;](/sql/dmx/functions-dmx)。  
  
 您还可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的预测查询生成器创建预测查询。  
  
## <a name="singleton-prediction-join-statement"></a>单独 PREDICTION JOIN 语句  
 第一步是通过使用**SELECT FROM \<MODEL> 预测联接**语法并提供一组值作为输入来创建单独查询。 下面是单独语句的一般示例：  
  
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
 您将在本课中执行以下任务：  
  
-   创建一个查询，根据客户购物车中现有的物品预测客户可能要购买的其他产品。 您将使用具有默认*MINIMUM_PROBABILITY*的挖掘模型创建此查询。  
  
-   根据客户购物车中的已有项创建一个查询，预测客户可能购买的其他项。 此查询基于一个不同的模型，在该模型中， *MINIMUM_PROBABILITY*已设置为0.01。 由于关联模型中*MINIMUM_PROBABILITY*的默认值为0.3，因此，对此模型的查询应返回比默认模型上的查询更多的可能项。  
  
## <a name="create-a-prediction-by-using-a-model-with-the-default-minimum_probability"></a>使用带有默认 MINIMUM_PROBABILITY 的模型创建预测  
  
#### <a name="to-create-an-association-query"></a>创建关联查询  
  
1.  在**对象资源管理器**中，右键单击实例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向 "**新建查询**"，然后单击 " **DMX** " 以打开查询编辑器。  
  
2.  将 `PREDICTION JOIN` 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    <select list>   
    ```  
  
     替换为：  
  
    ```  
    PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
     您可以只包括列名 [Products]，但通过使用 "[预测 &#40;DMX&#41;](/sql/dmx/predict-dmx)函数，您可以将该算法返回的产品数量限制为三个。 还可以使用 `INCLUDE_STATISTICS`，它将返回每种产品的支持、概率以及校正后的概率。 这些统计信息有助于您对预测的准确性进行分级。  
  
4.  将  
  
    ```  
    [<mining model>]   
    ```  
  
     替换为：  
  
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
  
     替换为：  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     此语句使用 `UNION` 语句来指定三种产品，这三种产品必须与预测的产品一起包含在购物车中。 
  `SELECT` 语句中的 Model 列对应于嵌套产品表中所包含的模型列。  
  
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
  
6.  在 "**文件**" 菜单上，单击 "**将 DMXQuery1 另存为**"。  
  
7.  在 "**另存为**" 对话框中，浏览到相应的文件夹，并将`Association Prediction.dmx`该文件命名为。  
  
8.  在工具栏上，单击 "**执行**" 按钮。  
  
     查询将返回包含以下三种产品的表：HL Mountain Tire、Fender Set – Mountain 和 ML Mountain Tire。 该表按概率顺序列出这些返回的产品。 最有可能包含在查询指定的三种产品所在购物车中的返回的产品将出现在表的顶部。 其次最有可能包含在购物车中的产品是下面的两种产品。 该表还包含说明预测准确性的统计信息。  
  
## <a name="create-a-prediction-by-using-a-model-with-a-minimum_probability-of-001"></a>使用 MINIMUM_PROBABILITY 为 0.01 的模型创建预测  
  
#### <a name="to-create-an-association-query"></a>创建关联查询  
  
1.  在**对象资源管理器**中，右键单击实例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向 "**新建查询**"，然后单击 " **DMX** " 以打开查询编辑器。  
  
2.  将 `PREDICTION JOIN` 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    <select list>   
    ```  
  
     替换为：  
  
    ```  
    PREDICT([Modified Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
4.  将  
  
    ```  
    [<mining model>]   
    ```  
  
     替换为：  
  
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
  
     替换为：  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     此语句使用 `UNION` 语句来指定三种产品，这三种产品必须与预测的产品一起包含在购物车中。 
  `[Model]` 语句中的 `SELECT` 列对应于嵌套产品表中的列。  
  
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
  
6.  在 "**文件**" 菜单上，单击 "**将 DMXQuery1 另存为**"。  
  
7.  在 "**另存为**" 对话框中，浏览到相应的文件夹，并将`Modified Association Prediction.dmx`该文件命名为。  
  
8.  在工具栏上，单击 "**执行**" 按钮。  
  
     查询将返回包含以下三种产品的表：HL Mountain Tire、Water Bottle 和 Fender Set - Mountain。 该表按概率顺序列出这些产品。 出现在该表顶部的产品是最有可能包含在查询指定的三种产品所在购物车中的产品。 其余产品是其次最有可能包含在该购物车中的产品。 该表还包含描述预测准确性的统计信息。  
  
     在此查询的结果中可以看到， *MINIMUM_PROBABILITY*参数的值会影响查询返回的结果。  
  
 这是市场篮教程中的最后一个步骤。 您现在即可拥有一组模型，并可通过该组模型预测客户可能同时购买的产品。  
  
 若要了解如何在另一个预测方案中使用 DMX，请参阅[自行车购买者 DMX 教程](../../2014/tutorials/bike-buyer-dmx-tutorial.md)。  
  
## <a name="see-also"></a>另请参阅  
 [关联模型查询示例](../../2014/analysis-services/data-mining/association-model-query-examples.md)   
 [数据挖掘查询接口](../../2014/analysis-services/data-mining/data-mining-query-tools.md)  
  
  
