---
title: 第5课：执行预测查询 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0037bd2f-aa2d-464b-bf86-b0210f0438b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a5f4d6dd79f62541e207df688349f694680e2421
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62822296"
---
# <a name="lesson-5-executing-prediction-queries"></a>第 5 课：执行预测查询
  在本课中，您将使用 SELECT 语句的 "[从\<模型> 预测联接（DMX）](/sql/dmx/select-from-model-cases-dmx) " 形式来创建两种不同类型的预测，这些预测基于您在[第2课：将挖掘模型添加到关联挖掘结构](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)中创建的决策树模型。 这些预测类型定义如下。  
  
 单独查询  
 使用单独查询可以在进行预测时提供即席值。 例如，您可以通过将输入（如客户的上下班路程、区号或子女数）传递给查询来确定一个客户是否会购买自行车。 单独查询可基于这些输入，返回指示客户购买自行车的可能性大小的值。  
  
 批查询  
 使用批查询可确定潜在客户表中的哪个人可能购买自行车。 例如，如果市场部提供客户及客户属性的列表，那么您可以使用批预测确定该表中的哪个人可能购买自行车。  
  
 SELECT 语句的[ \<select FROM MODEL> 预测联接（DMX）](/sql/dmx/select-from-model-cases-dmx)形式包含三个部分：  
  
-   结果中返回的挖掘模型列和预测函数列表。 结果还可以包含源数据中的输入列。  
  
-   定义要用于创建预测的数据的源查询。 例如，在批查询中，此部分可能是客户列表。  
  
-   挖掘模型列和源数据之间的映射。 如果这些名称匹配，则可以使用 NATURAL 语法并且不考虑列映射。  
  
 可以使用预测函数进一步增强查询功能。 预测函数提供其他信息（例如预测出现的概率），并支持在定型数据集中进行预测。 有关预测函数的详细信息，请参阅[函数 &#40;DMX&#41;](/sql/dmx/functions-dmx)。  
  
 本教程中的预测基于 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 示例数据库中的 ProspectiveBuyer 表。 ProspectiveBuyer 表包含潜在客户及其关联特征的列表。 此表中的客户与用来创建决策树挖掘模型的客户无关。  
  
 您还可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中使用预测查询生成器创建预测。  
  
## <a name="lesson-tasks"></a>课程任务  
 您将在本课中执行以下任务：  
  
-   创建一个单独查询，以确定特定客户是否可能购买自行车  
  
-   创建一个批查询，以确定客户表中列出客户中哪些可能会购买自行车。  
  
## <a name="singleton-query"></a>单独查询  
 第一步是在单独预测查询中使用[SELECT FROM &#60;模型&#62; 预测联接 &#40;DMX&#41;](/sql/dmx/select-from-model-cases-dmx) 。 下面是单独语句的一般示例：  
  
```  
SELECT <select list> FROM [<mining model name>]   
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
```  
  
 代码的第一行定义查询应返回的挖掘模型中的列，并指定用于生成预测的挖掘模型的名称：  
  
```  
SELECT <select list> FROM [<mining model name>]   
```  
  
 代码接下来的各行定义用于创建预测的客户的特征：  
  
```  
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
ORDER BY <expression>  
```  
  
 如果指定 NATURAL PREDICTION JOIN，则服务器会基于列名，尝试将模型的每列与输入的列进行匹配。 如果列名不匹配，则忽略这些列。  
  
#### <a name="to-create-a-singleton-prediction-query"></a>创建单独预测查询  
  
1.  在**对象资源管理器**中，右键单击实例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向 "**新建查询**"，然后单击 " **DMX**"。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  将单独语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    <select list>   
    ```  
  
     替换为：  
  
    ```  
    [Bike Buyer] AS Buyer, PredictHistogram([Bike Buyer]) AS Statistics  
    ```  
  
     AS 语句用于查询返回的别名列。 [PredictHistogram](/sql/dmx/predicthistogram-dmx)函数返回有关预测的统计信息，包括概率和支持。 有关可在预测语句中使用的函数的详细信息，请参阅[函数 &#40;DMX&#41;](/sql/dmx/functions-dmx)。  
  
4.  将  
  
    ```  
    [<mining model>]   
    ```  
  
     替换为：  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  将  
  
    ```  
    (SELECT '<value>' AS [<column name>], ...)  AS t  
    ```  
  
     替换为：  
  
    ```  
    (SELECT 35 AS [Age],  
      '5-10 Miles' AS [Commute Distance],  
      '1' AS [House Owner Flag],  
      2 AS [Number Cars Owned],  
      2 AS [Total Children]) AS t  
    ```  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    SELECT  
       [Bike Buyer] AS Buyer,  
       PredictHistogram([Bike Buyer]) AS Statistics  
    FROM  
       [Decision Tree]  
    NATURAL PREDICTION JOIN  
    (SELECT 35 AS [Age],  
       '5-10 Miles' AS [Commute Distance],  
       '1' AS [House Owner Flag],  
       2 AS [Number Cars Owned],  
       2 AS [Total Children]) AS t  
    ```  
  
6.  在 "**文件**" 菜单上，单击 "**将 DMXQuery1 另存为**"。  
  
7.  在 "**另存为**" 对话框中，浏览到相应的文件夹，并将`Singleton_Query.dmx`该文件命名为。  
  
8.  在工具栏上，单击 "**执行**" 按钮。  
  
     查询将返回有关具有指定特征的客户是否会购买自行车的预测，以及有关此预测的统计信息。  
  
## <a name="batch-query"></a>批查询  
 下一步是使用批预测查询中[&#60;模型&#62; 预测联接 &#40;DMX&#41;](/sql/dmx/select-from-model-cases-dmx) 。 下面是批语句的一般示例：  
  
```  
SELECT TOP <number> <select list>   
FROM [<mining model name>]  
PREDICTION JOIN  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
ON <on clause, mapping,>  
WHERE <where clause, boolean expression,>  
ORDER BY <expression>  
```  
  
 与在单独查询中相同，代码的前两行定义查询返回的挖掘模型的列，以及用于生成预测的挖掘模型的名称。 TOP \<number> 语句指定查询将只返回 number> 指定\<的数字或结果。  
  
 代码的接下来各行定义预测所基于的源数据：  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
```  
  
 您可以使用多种方法检索源数据，但是在本教程中，您将使用 OPENQUERY。 有关可用选项的详细信息，请参阅[&#60;源数据查询&#62;](/sql/dmx/source-data-query)。  
  
 下一行定义挖掘模型中的源列和源数据中的列之间的映射：  
  
```  
ON <column mappings>  
```  
  
 WHERE 子句筛选预测查询返回的结果：  
  
```  
WHERE <where clause, boolean expression,>  
```  
  
 代码的最后一行和可选行指定排列结果所依据的列：  
  
```  
ORDER BY <expression> [DESC|ASC]  
```  
  
 使用 ORDER BY 结合 TOP \<number> 语句来筛选返回的结果。 例如，在此预测中，您将返回前十位自行车购买者，他们按照正确的预测概率排列。 您可以使用 [DESC|ASC] 语法控制结果的显示顺序。  
  
#### <a name="to-create-a-batch-prediction-query"></a>创建批预测查询  
  
1.  在**对象资源管理器**中，右键单击实例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向 "**新建查询**"，然后单击 " **DMX**"。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  将批语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    <select list>   
    ```  
  
     替换为：  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    ```  
  
     TOP 10 子句指定查询只返回前十个结果。 此查询中的 ORDER BY 语句按照正确的预测概率排列结果，因此只返回前十个最可能的结果。  
  
4.  将以下占位符  
  
    ```  
    [<mining model>]   
    ```  
  
     替换为模型的名称：  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  将以下一般 OPENQUERY 语句  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     替换为引用当前 Adventureworks 数据仓库的语句，例如：  
  
    ```  
    OPENQUERY([Adventure Works DW 2014],  
      'SELECT  
        [LastName],  
        [FirstName],  
        [MaritalStatus],  
        [Gender],  
        [YearlyIncome],  
        [TotalChildren],  
        [NumberChildrenAtHome],  
        [Education],  
        [Occupation],  
        [HouseOwnerFlag],  
        [NumberCarsOwned]  
      FROM  
        [dbo].[ProspectiveBuyer]  
      ') AS t  
    ```  
  
6.  将以下一般语法  
  
    ```  
    <ON clause, mapping,>   
    WHERE <where clause, boolean expression,>  
    ORDER BY <expression>  
    ```  
  
     替换为此模型和输入数据集所需的列映射：  
  
    ```  
    [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
     指定 `DESC` 以便首先列出概率最大的结果。  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    FROM  
      [Decision Tree]  
    PREDICTION JOIN  
      OPENQUERY([Adventure Works DW 2014],  
        'SELECT  
          [LastName],  
          [FirstName],  
          [MaritalStatus],  
          [Gender],  
          [YearlyIncome],  
          [TotalChildren],  
          [NumberChildrenAtHome],  
          [Education],  
          [Occupation],  
          [HouseOwnerFlag],  
          [NumberCarsOwned]  
        FROM  
          [dbo].[ProspectiveBuyer]  
        ') AS t  
    ON  
      [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
7.  在 "**文件**" 菜单上，单击 "**将 DMXQuery1 另存为**"。  
  
8.  在 "**另存为**" 对话框中，浏览到相应的文件夹，并将`Batch_Prediction.dmx`该文件命名为。  
  
9. 在工具栏上，单击 "**执行**" 按钮。  
  
     查询将返回一个表，其中包含客户名称、每位客户是否将购买自行车的预测，以及该预测的概率。  
  
 这是自行车购买者教程中的最后一个步骤。 现在，您拥有一个挖掘模型集，可以使用它们来浏览客户之间的相似之处并预测潜在客户是否将购买自行车。  
  
 若要了解如何在市场篮方案中使用 DMX，请参阅[市场篮 DMX 教程](../../2014/tutorials/market-basket-dmx-tutorial.md)。  
  
  
