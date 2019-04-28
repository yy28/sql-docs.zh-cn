---
title: SELECT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: def96304f13f57095679056e6eab0a004b5c47d9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62658754"
---
# <a name="select-dmx"></a>SELECT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **选择**语句中的数据挖掘扩展插件 (DMX) 用于数据挖掘中的以下任务：  
  
-   浏览现有挖掘模型的内容  
  
-   根据现有挖掘模型创建预测  
  
-   创建现有挖掘模型的副本  
  
-   浏览挖掘结构  
  
 尽管该语句的完整语法很复杂，但用于浏览模型及其基础结构的一级子句可以概括如下：  
  
```  
SELECT [FLATTENED] [TOP <n>] <select list>  
FROM <model/structure>[.aspect]  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
## <a name="flattened"></a>FLATTENED  
 有些数据挖掘客户端无法接受数据挖掘提供程序提供的、层次结构格式的结果集。 客户端可能不具备处理层次结构的能力，或者可能必须将结果存储在单一非规范化表中。 若要将嵌套表数据转换为平展表数据，您必须请求平展查询结果。  
  
 若要平展查询结果，请使用**选择**语法**FLATTENED**选项，如下面的示例中所示：  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>顶部\<n > 和 ORDER BY  
 可以使用一个表达式，排序查询的结果，然后可以通过结合使用返回的结果子集**ORDER BY**并**顶部**子句。 如果在确定邮件目标时，只想将结果发送给最可能的答复者，以及类似的情况，上述选项就很有用。 可能的目标邮递按预测概率的预测查询结果进行排序，然后仅返回顶部\<n > 结果。  
  
## <a name="select-list"></a>选择列表  
 *\<选择列表 >* 可包括标量列引用、 预测函数和表达式。 可用的选项取决于算法以及下列上下文：  
  
-   是否正在查询挖掘结构或挖掘模型  
  
-   是否正在查询内容或事例  
  
-   源数据是关系表还是多维数据集  
  
-   是否正在进行预测  
  
 在很多情况下，您可以使用别名，或者根据选择列表中的项创建简单表达式。 例如，下面的示例显示一个基于模型列的简单表达式：  
  
```  
SELECT [CustomerID], [Last Name] + ', ' + [FirstName] AS FullName  
FROM <model>.CASES  
```  
  
 下面的示例为包含预测函数的结果的列创建一个别名：  
  
```  
SELECT Predict([Column1], 'Value') as Column1Prediction  
FROM MyModel  
JOIN <source data query>  
```  
  
## <a name="where"></a>WHERE  
 您可以限制查询返回使用的事例**其中**子句。 **其中**子句指定中的列引用**其中**表达式必须具有相同的语义中的列引用*\<选择列表 >* 的**选择**语句，并且只能返回一个布尔表达式。 语法**其中**子句如下所示  
  
```  
WHERE < condition expression >  
```  
  
 选择列表和**其中**子句**选择**语句必须遵循以下规则：  
  
-   选择列表必须包含一个不返回布尔值结果的表达式。 可以修改该表达式，但该表达式必须返回非布尔值结果。  
  
-   **其中**子句必须包含一个表达式，返回布尔值结果。 可以修改该子句，但该子句必须返回布尔值结果。  
  
## <a name="predictions"></a>预测  
 创建预测时可以使用以下两种类型的语法：  
  
-   [SELECT FROM &#60;model&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [SELECT FROM &#60;model&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 使用第一种预测类型可以实时或按批创建复杂预测。  
  
 第二种预测类型可以对挖掘模型中的可预测列创建空预测联接，并返回该列的最可能状态。 该查询的结果完全取决于挖掘模型的内容。  
  
 您可以通过使用以下语法为 select 语句插入 SELECT FROM PREDICTION JOIN 语句的源查询。  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 有关创建预测查询的详细信息，请参阅[结构和 DMX 预测查询的使用情况](../dmx/structure-and-usage-of-dmx-prediction-queries.md)。  
  
## <a name="clause-syntax"></a>子句语法  
 由于下进行浏览的复杂性**选择**按子句说明语句、 详细的语法元素和参数。 有关各个子句的详细信息，请单击下面列表中的主题：  
  
 [SELECT DISTINCT FROM &#60;model &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [SELECT FROM &#60;model&#62;.CONTENT &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
 [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [SELECT FROM &#60;model&#62;.SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [SELECT FROM &#60;model&#62;.DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [SELECT FROM &#60;model&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [SELECT FROM &#60;model&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 [SELECT FROM &#60;structure&#62;.CASES](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)  
  
  
