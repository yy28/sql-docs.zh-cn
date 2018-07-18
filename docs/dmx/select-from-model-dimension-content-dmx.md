---
title: SELECT FROM&lt;模型&gt;。DIMENSION_CONTENT (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29f730f0bdff985ffceb849c429e5d1b02f70d5f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37992621"
---
# <a name="select-from-ltmodelgtdimensioncontent-dmx"></a>SELECT FROM&lt;模型&gt;。DIMENSION_CONTENT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  挖掘模型可用作 OLAP 多维数据集中的一个维度，模型中的每个节点表示一个维度成员。 **SELECT FROM\<模型 >。Dimension_CONTENT**语句可以返回模型中的维度用法相关的内容。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.Dimension_CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>参数  
 *n*  
 可选。 一个指定返回行数的整数。  
  
 *表达式列表*  
 基于内容架构行集派生的一组以逗号分隔的相关列标识符。  
  
 *model*  
 模型标识符。  
  
 *条件表达式*  
 可选。 一个限制条件，用于限制从列列表返回的值。  
  
 *expression*  
 可选。 一个返回标量值的表达式。  
  
## <a name="remarks"></a>Remarks  
 算法提供程序定义要返回的内容以及这些内容的组织方式。 例如，提供程序可能会限制维度内容中说明的节点数。  
  
 下表列出了可进行维度内容查询的列，以及每个列作为数据挖掘维度来执行的函数。  
  
|CONTENT 行集列|数据挖掘维度中的函数|  
|---------------------------|---------------------------------------|  
|ATTRIBUTE_NAME|成员属性。|  
|NODE_NAME|成员属性。|  
|NODE_UNIQUE_NAME|键属性。|  
|NODE_TYPE|成员属性。|  
|NODE_CAPTION|有关 CaptionColumn**密钥**属性。|  
|CHILDREN_CARDINALITY|成员属性。|  
|PARENT_UNIQUE_NAME|有关 RelatedAttribute**密钥**属性 (父-子层次结构中的 ParentAttribute)。|  
|NODE_DESCRIPTION|成员属性。|  
|NODE_RULE|成员属性。|  
|MARGINAL_RULE|成员属性。|  
|NODE_PROBABILITY|成员属性。|  
|MARGINAL_PROBABILITY|成员属性。|  
|NODE_SUPPORT|成员属性。|  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>Description  
 该示例从 `[TM Decision Tree]` 模型内容中选择了所有列，这些模型内容与用作维度的模型相关。  
  
### <a name="code"></a>代码  
  
```  
SELECT *   
FROM [TM Decision Tree].Dimension_Content  
```  
  
## <a name="see-also"></a>请参阅  
 [选择&AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
