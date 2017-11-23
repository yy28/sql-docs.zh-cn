---
title: "选择 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: SELECT
dev_langs: DMX
helpviewer_keywords:
- browsing mining model [Analysis Services]
- TOP clause, SELECT
- FLATTENED option
- predictions [DMX]
- ORDER BY clause [DMX]
- SELECT statement [DMX]
- mining models [Analysis Services], browsing
- statements [DMX], SELECT statement
- WHERE clause, DMX
ms.assetid: 32d9e8fd-796b-4e1c-ae59-73cd6f645485
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 79fb3f8ce7766130ced9a8353a83e34bbbf007d1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="select-dmx"></a>SELECT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **选择**语句中数据挖掘扩展插件 (DMX) 用于数据挖掘中的以下任务：  
  
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
  
 若要对查询结果进行平展，使用**选择**语法与**FLATTENED**选项，如下面的示例中所示：  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>顶部\<n > 和排序依据  
 你可以通过使用表达式，排序查询的结果，然后可以通过结合使用返回的结果子集**ORDER BY**和**顶部**子句。 如果在确定邮件目标时，只想将结果发送给最可能的答复者，以及类似的情况，上述选项就很有用。 无法按预测概率，邮件预测查询的目标的结果进行排序，然后仅返回顶部\<n > 结果。  
  
## <a name="select-list"></a>选择列表  
 *\<选择列表 >*可以包含标量列引用、 预测函数和表达式。 可用的选项取决于算法以及下列上下文：  
  
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
 你可以限制查询返回使用的事例**其中**子句。 **其中**子句指定中引用该列**其中**表达式必须具有与中的列引用相同的语义*\<选择列表 >*的**选择**语句，并可以仅返回一个布尔表达式。 语法**其中**子句，如下所示是  
  
```  
WHERE < condition expression >  
```  
  
 选择列表和**其中**子句**选择**语句必须遵循以下规则：  
  
-   选择列表必须包含一个不返回布尔值结果的表达式。 可以修改该表达式，但该表达式必须返回非布尔值结果。  
  
-   **其中**子句必须包含一个表达式，返回布尔值结果。 可以修改该子句，但该子句必须返回布尔值结果。  
  
## <a name="predictions"></a>预测  
 创建预测时可以使用以下两种类型的语法：  
  
-   [选择从和 #60; 模型 &#62;预测联接 &#40; DMX &#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [选择从和 #60; 模型 &#62;&#40; DMX &#41;](../dmx/select-from-model-dmx.md)  
  
 使用第一种预测类型可以实时或按批创建复杂预测。  
  
 第二种预测类型可以对挖掘模型中的可预测列创建空预测联接，并返回该列的最可能状态。 该查询的结果完全取决于挖掘模型的内容。  
  
 你可以通过使用以下语法将插入选择从 PREDICTION JOIN 语句的源查询的 select 语句。  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 有关创建预测查询的详细信息，请参阅[结构和 DMX 预测查询的使用情况](../dmx/structure-and-usage-of-dmx-prediction-queries.md)。  
  
## <a name="clause-syntax"></a>子句语法  
 由于浏览与复杂性**选择**语句、 详细的语法元素和自变量均由子句描述。 有关各个子句的详细信息，请单击下面列表中的主题：  
  
 [SELECT DISTINCT FROM #60; 模型 &#62;&#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [SELECT FROM &#60; 模型 &#62;。内容 &#40; DMX &#41;](../dmx/select-from-model-content-dmx.md)  
  
 [SELECT FROM &#60; 模型 &#62;。用例 &#40; DMX &#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [SELECT FROM &#60; 模型 &#62;。SAMPLE_CASES &#40; DMX &#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [SELECT FROM &#60; 模型 &#62;。DIMENSION_CONTENT &#40; DMX &#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [选择从和 #60; 模型 &#62;预测联接 &#40; DMX &#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [选择从和 #60; 模型 &#62;&#40; DMX &#41;](../dmx/select-from-model-dmx.md)  
  
 [SELECT FROM &#60; 结构 &#62;。用例](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)  
  
  
