---
title: "SELECT FROM&lt;模型&gt;。内容 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT
- FROM
- Content
dev_langs: DMX
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- SELECT FROM <model>.CONTENT statement
ms.assetid: a270b33f-77be-41fa-9340-2f6cb0dd75e5
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 24b5a1884994050874cbfd24afbae84b773620d1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="select-from-ltmodelgtcontent-dmx"></a>SELECT FROM&lt;模型&gt;。内容 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回指定数据挖掘模型的挖掘模型架构行集。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>参数  
 *n*  
 可选。 一个指定返回行数的整数。  
  
 *表达式列表*  
 从内容架构行集派生的一组列，各列间以逗号分隔。  
  
 *model*  
 一个模型标识符。  
  
 *条件表达式*  
 可选。 一个限制条件，用于限制从列列表返回的值。  
  
 *expression*  
 可选。 一个返回标量值的表达式。  
  
## <a name="remarks"></a>Remarks  
 The **SELECT FROM** *\<model>***.内容**语句返回特定于每种算法的内容。 例如，您可能希望在自定义应用程序中，使用某个关联规则模型的所有规则的说明。 你可以使用**SELECT FROM\<模型 >。内容**语句以返回模型的 NODE_RULE 列中值。  
  
 下表列出了挖掘模型内容中包含的列。  
  
> [!NOTE]  
>  算法可能会为了正确表示内容而对列做出不同的解释。 挖掘模型内容每个算法，以及如何解释和查询挖掘模型内容的每个模型类型提示的说明，请参阅[挖掘模型内容 &#40;Analysis Services-数据挖掘 &#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
|CONTENT 行集列|Description|  
|---------------------------|-----------------|  
|MODEL_CATALOG|目录名称。 如果提供程序不支持目录，则为 NULL。|  
|MODEL_SCHEMA|未限定的架构名称。 如果提供程序不支持架构，则为 NULL。|  
|MODEL_NAME|模型名称。 此列中不能包含 NULL。|  
|ATTRIBUTE_NAME|与节点相对应的属性的名称。|  
|NODE_NAME|节点的名称。|  
|NODE_UNIQUE_NAME|节点在模型中的唯一名称。|  
|NODE_TYPE|表示节点类型的整数。 实例时都提供 SQL Server 登录名。|  
|NODE_GUID|节点 GUID。 如果没有 GUID，则为 NULL。|  
|NODE_CAPTION|与节点关联的标签或标题， 主要用于显示目的。 如果不存在标题，则返回 NODE_NAME。|  
|CHILDREN_CARDINALITY|节点所具有的子节点的数目。|  
|PARENT_UNIQUE_NAME|节点的父节点的唯一名称。|  
|NODE_DESCRIPTION|节点的说明。|  
|NODE_RULE|表示嵌入在节点中的规则的 XML 片段。 XML 字符串的格式采用 PMML 标准。|  
|MARGINAL_RULE|说明从父节点到节点的路径的 XML 片段。|  
|NODE_PROBABILITY|路径在节点中结束的概率。|  
|MARGINAL_PROBABILITY|从父节点到达该节点的概率。|  
|NODE_DISTRIBUTION|包含说明节点中值分布的统计信息的表。|  
|NODE_SUPPORT|支持此节点的事例数。|  
  
## <a name="examples"></a>示例  
 下面的代码返回已添加到目标邮件挖掘结构的决策树模型的父节点 ID。  
  
```  
SELECT MODEL_NAME, NODE_NAME FROM [TM Decision Tree].CONTENT  
WHERE NODE_TYPE = 1  
```  
  
 预期的结果：  
  
|MODEL_NAME|NODE_NAME|  
|-----------------|----------------|  
|TM_DecisionTree|0|  
  
 下面的查询使用**IsDescendant**函数以返回在前面的查询返回的节点的直属子对象。  
  
> [!NOTE]  
>  因为 NODE_NAME 的值是字符串，不能使用嵌套 select 语句的自变量作为返回，通过 NODE_ID **IsDescendant**函数。  
  
```  
SELECT NODE_NAME, NODETYPE, NODE_CAPTION   
FROM [TM Decision Tree].CONTENT  
WHERE ISDESCENDANT('0')  
```  
  
 预期的结果：  
  
 由于该模型是一个决策树模型，所以模型父节点的后代中包含一个边际统计信息节点、一个表示可预测属性的节点以及多个包含输入属性和值的节点。 有关详细信息，请参阅[决策树模型的挖掘模型内容（Analysis Services - 数据挖掘）](../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)。  
  
## <a name="using-the-flattened-keyword"></a>使用 FLATTENED 关键字  
 挖掘模型内容常常将模型的相关重要信息包含在嵌套表列中。 您可以使用 FLATTENED 关键字，从嵌套表列中检索数据，而无需使用支持分层行集的提供程序。  
  
 下面的查询从 Naïve Bayes 模型返回一个单个节点：边际统计信息节点 (NODE_TYPE = 26)。 此节点的 NODE_DISTRIBUTION 列中包含一个嵌套表。 因此，对该嵌套表列进行了平展，对于该嵌套表的每一行，均相应地返回了一行。 对于该嵌套表中的每一行，标量列 MODEL_NAME 的值都重复了一次。  
  
 另请注意：如果只指定嵌套表列的名称，则将会针对嵌套表中的每一列返回一个新列。 默认情况下，嵌套表的名称作为每个嵌套表列名称的前缀。  
  
```  
SELECT FLATTENED MODEL_NAME, NODE_DISTRIBUTION  
FROM [TM_NaiveBayes].CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 示例结果：  
  
|MODEL_NAME|NODE_DISTRIBUTION.ATTRIBUTE_NAME|NODE_DISTRIBUTION.ATTRIBUTE_VALUE|NODE_DISTRIBUTION.SUPPORT|NODE_DISTRIBUTION.PROBABILITY|NODE_DISTRIBUTION.VARIANCE|NODE_DISTRIBUTION.VALUETYPE|  
|-----------------|----------------------------------------|-----------------------------------------|--------------------------------|------------------------------------|---------------------------------|----------------------------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|0|@shouldalert|  
|TM_NaiveBayes|Bike Buyer|0|6556|0.506685215240745|0||  
|TM_NaiveBayes|Bike Buyer|@shouldalert|6383|0.493314784759255|0||  
  
 下面的示例演示如何使用嵌套 select 语句，仅从嵌套表返回部分列。 您可以通过对嵌套表的表名使用别名来简化显示，如下所示。  
  
```  
SELECT MODEL_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT] AS t  
FROM NODE_DISTRIBUTION)   
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 示例结果：  
  
|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|  
|-----------------|-----------------------|------------------------|---------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|  
|TM_NaiveBayes|Bike Buyer|0|6556|  
|TM_NaiveBayes|Bike Buyer|@shouldalert|6383|  
  
## <a name="see-also"></a>另请参阅  
 [选择 &#40; DMX &#41;](../dmx/select-dmx.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
