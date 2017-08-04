---
title: "SELECT FROM&lt;模型&gt;预测联接 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PREDICTION
- PREDICTION_JOIN
- SELECT
- join
- FROM
- PREDICTION JOIN
dev_langs:
- DMX
helpviewer_keywords:
- prediction joins [DMX]
- PREDICTION JOIN statement
- natural prediction joins [DMX]
- open query predictions
- singleton query predictions [DMX]
- SELECT FROM <model> PREDICTION JOIN statement
ms.assetid: 7ca37fec-4a50-4d79-b1d6-1c7c12176946
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7caf239374a174cc26c2bee349c1a52c805f4de4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgt-prediction-join-dmx"></a>SELECT FROM&lt;模型&gt;预测联接 (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用挖掘模型来预测外部数据源中的列状态。 **PREDICTION JOIN**语句与匹配的源查询从每个用例与该模型。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <select expression list>   
FROM <model> | <sub select> [NATURAL] PREDICTION JOIN   
<source data query> [ON <join mapping list>]   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>参数  
 *n*  
 選擇性。 一个指定返回行数的整数。  
  
 *选择的表达式列表*  
 从挖掘模型中派生的一组以逗号分隔的列标识符和表达式。  
  
 *model*  
 一个模型标识符。  
  
 *sub 选择*  
 嵌入的 Select 语句。  
  
 *源数据查询*  
 源查询。  
  
 *联接映射列表*  
 選擇性。 一种逻辑表达式，可以将模型中的列与源查询中的列进行比较。  
  
 *条件表达式*  
 選擇性。 一个限制条件，用于限制从列列表返回的值。  
  
 *expression*  
 選擇性。 一个返回标量值的表达式。  
  
## <a name="remarks"></a>注释  
 ON 子句定义了源查询中的列与挖掘模型中的列之间的映射。 该映射用于将源查询中的列定向到挖掘模型中的列，这样便可将这些列用作输入以便创建预测。 中的列\<*联接映射列表*> 相关使用等号 （=），如下面的示例中所示：  
  
```  
[MiningModel].ColumnA = [source data query].Column1 AND   
[MiningModel].ColumnB = [source data query].Column2 AND  
...  
```  
  
 如果要在 ON 子句中绑定一个嵌套表，请确保将键列与非键列进行绑定，以便算法可以正确地标识嵌套列记录所属的事例。  
  
 用于预测联接的源查询可以是表，也可以是单独查询。  
  
 你可以指定不返回表表达式中的预测函数\< *select 表达式列表*> 和\<*条件表达式*>。  
  
 **NATURAL PREDICTION JOIN**自动映射在一起的源查询从模型中的列名称匹配的列名称。 如果你使用**自然预测**，则可以省略 ON 子句。  
  
 WHERE 条件只能用于可预测列或相关列。  
  
 ORDER by 子句可以接受只有一个列作为参数;也就是说，不能在多个列进行排序。  
  
## <a name="example-1-singleton-query"></a>示例 1：单独查询  
 下面的示例演示如何创建用于实时预测某个人是否会购买自行车的查询。 在此查询中，数据没有存储在表或其他数据源中，而是直接输入到查询中。 查询中的人员具有下列特性：  
  
-   35 岁  
  
-   拥有一套住房  
  
-   拥有两部汽车  
  
-   有两个子居住在家里项  
  
 使用 TM 决策树挖掘模型和使用者有关的已知的特征，查询将返回一个布尔值，描述用户购买了自行车和表格返回的值，通过一组[PredictHistogram &#40; DMX &#41;](../dmx/predicthistogram-dmx.md)函数，用于描述进行预测的方式。  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  PredictHistogram([Bike Buyer])  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 35 AS [Age],  
  '5-10 Miles' AS [Commute Distance],  
  '1' AS [House Owner Flag],  
  2 AS [Number Cars Owned],  
  2 AS [Total Children]) AS t  
```  
  
## <a name="example-2-using-openquery"></a>示例 2：使用 OPENQUERY  
 下面的示例演示如何创建批预测查询中使用存储在外部数据集的潜在客户的列表。 因为该表是已定义的实例的数据源视图的一部分[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，查询无法使用[OPENQUERY](../dmx/source-data-query-openquery.md)检索的数据。 因为表中的列的名称不同于在挖掘模型中， **ON**子句必须用于表中的列映射到模型中的列。  
  
 查询返回表中每个人的姓氏和名字，以及指示每个人是否会购买自行车的布尔列；其中，0 表示“可能不会购买自行车”，1 表示“可能会购买自行车”。 最后一列包含预测结果的概率。  
  
```  
SELECT  
  t.[LastName],  
  t.[FirstName],  
  [TM Decision Tree].[Bike Buyer],  
  PredictProbability([Bike Buyer])  
From  
  [TM Decision Tree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
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
  [TM Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
  [TM Decision Tree].[Gender] = t.[Gender] AND  
  [TM Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM Decision Tree].[Total Children] = t.[TotalChildren] AND  
  [TM Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM Decision Tree].[Education] = t.[Education] AND  
  [TM Decision Tree].[Occupation] = t.[Occupation] AND  
  [TM Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
```  
  
 若要将数据集限制为仅包含经预测可能会购买自行车的客户，然后按照客户的名称对列表进行排序，则可向前一个示例中添加一个 WHERE 子句和一个 ORDER BY 子句：  
  
```  
WHERE [BIKE Buyer]  
ORDER BY [LastName] ASC  
```  
  
## <a name="example-3-predicting-associations"></a>示例 3：预测关联  
 下例说明如何使用由 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联算法生成的模型创建预测。 关联模型生成的预测可用于推荐相关产品。 例如，下面的查询返回三种产品，购买这三种产品的同时最有可能还会一起购买以下产品：  
  
-   Mountain Bottle Cage  
  
-   Mountain Tire Tube  
  
-   Mountain-200  
  
 [预测 &#40; DMX &#41;](../dmx/predict-dmx.md)函数是多态类型，可以用于所有模型类型。 可以使用 value3 作为函数的参数来限制查询返回的项的数目。 **选择**遵循 NATURAL PREDICTION JOIN 子句的列表提供要使用作为输入来预测的值。  
  
```  
SELECT FLATTENED  
  PREDICT([Association].[v Assoc Seq Line Items], 3)  
FROM  
  [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
  UNION SELECT 'Mountain Tire Tube' AS [Model]  
  UNION SELECT 'Mountain-200' AS [Model]) AS [v Assoc Seq Line Items ]) AS t  
```  
  
 示例结果：  
  
|Expression.Model|  
|----------------------|  
|HL Mountain Tire|  
|Water Bottle|  
|Fender Set - Mountain|  
  
 由于包含可预测属性 `[v Assoc Seq Line Items]` 的列是一个表列，因此查询将返回一个包含嵌套表的列。 默认情况下，嵌套表列名为 `Expression`。 如果你的提供程序不支持分层行集，则可以使用**FLATTENED**关键字，如要使结果更轻松地查看在此示例中所示。  
  
## <a name="see-also"></a>另請參閱  
 [选择 &#40; DMX &#41;](../dmx/select-dmx.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

