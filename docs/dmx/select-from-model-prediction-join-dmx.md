---
title: 从模型&lt;&gt;预测联接（DMX）中选择 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b592aef0ba3831c5513e039ee4552d826468e819
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67928332"
---
# <a name="select-from-ltmodelgt-prediction-join-dmx"></a>选择&lt;模型&gt;预测联接（DMX）
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  使用挖掘模型来预测外部数据源中的列状态。 此**预测联接**语句将源查询中的每个事例与该模型匹配。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <select expression list>   
FROM <model> | <sub select> [NATURAL] PREDICTION JOIN   
<source data query> [ON <join mapping list>]   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>参数  
 *n*  
 可选。 一个指定返回行数的整数。  
  
 *选择表达式列表*  
 从挖掘模型中派生的一组以逗号分隔的列标识符和表达式。  
  
 *模型*  
 模型标识符。  
  
 *子选择*  
 嵌入的 Select 语句。  
  
 *源数据查询*  
 源查询。  
  
 *联接映射列表*  
 可选。 一种逻辑表达式，可以将模型中的列与源查询中的列进行比较。  
  
 *条件表达式*  
 可选。 一个限制条件，用于限制从列列表返回的值。  
  
 *expression*  
 可选。 一个返回标量值的表达式。  
  
## <a name="remarks"></a>备注  
 ON 子句定义了源查询中的列与挖掘模型中的列之间的映射。 该映射用于将源查询中的列定向到挖掘模型中的列，这样便可将这些列用作输入以便创建预测。 \<*联接映射列表*中的列> 通过使用等号（=）进行关联，如下面的示例中所示：  
  
```  
[MiningModel].ColumnA = [source data query].Column1 AND   
[MiningModel].ColumnB = [source data query].Column2 AND  
...  
```  
  
 如果要在 ON 子句中绑定一个嵌套表，请确保将键列与非键列进行绑定，以便算法可以正确地标识嵌套列记录所属的事例。  
  
 用于预测联接的源查询可以是表，也可以是单独查询。  
  
 您可以在 " \<*选择表达式" 列表*中指定不返回表表达式> 和\<*条件表达式*> 的预测函数。  
  
 **自然预测联接**自动将源查询中的列名称与模型中的列名称相匹配。 如果使用**自然预测**，则可以省略 ON 子句。  
  
 WHERE 条件只能用于可预测列或相关列。  
  
 ORDER by 子句只能接受单个列作为参数;也就是说，不能对多个列进行排序。  
  
## <a name="example-1-singleton-query"></a>示例 1：单独查询  
 下面的示例演示如何创建用于实时预测某个人是否会购买自行车的查询。 在此查询中，数据没有存储在表或其他数据源中，而是直接输入到查询中。 查询中的人员具有下列特性：  
  
-   35 岁  
  
-   拥有一套住房  
  
-   拥有两部汽车  
  
-   在家中有两个子项  
  
 通过使用 TM 决策树挖掘模型和有关使用者的已知特征，该查询将返回一个布尔值，该布尔值用于描述此人是否购买了自行车以及一组用于说明如何进行预测的[PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md)函数返回的表格值。  
  
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
 下面的示例演示如何通过使用存储在外部数据集中的潜在客户列表来创建批预测查询。 由于表是在实例上定义的数据源视图的一部分[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，因此查询可以使用[OPENQUERY](../dmx/source-data-query-openquery.md)检索数据。 因为表中各列的名称与挖掘模型中的列的名称不同，所以必须使用**ON**子句将表中的列映射到模型中的列。  
  
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
  
 [预测 &#40;DMX&#41;](../dmx/predict-dmx.md)函数是多态函数，可用于所有模型类型。 可以使用 value3 作为函数的参数来限制查询返回的项的数目。 在自然预测联接子句之后的**选择**列表提供了要用作预测输入的值。  
  
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
  
 由于包含可预测属性 `[v Assoc Seq Line Items]` 的列是一个表列，因此查询将返回一个包含嵌套表的列。 默认情况下，嵌套表列名为 `Expression`。 如果提供程序不支持分层行集，则可以使用此示例中所示的**平展**关键字来使结果更易于查看。  
  
## <a name="see-also"></a>另请参阅  
 [选择 &#40;DMX&#41;](../dmx/select-dmx.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
