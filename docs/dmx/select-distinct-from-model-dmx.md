---
title: "SELECT DISTINCT FROM&lt;模型&gt;(DMX) |Microsoft 文档"
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
f1_keywords:
- DISTINCT
- SELECT
dev_langs: DMX
helpviewer_keywords:
- discrete columns [DMX]
- discretized columns [DMX]
- SELECT DISTINCT FROM <model> statement
- continuous columns
ms.assetid: 0ab44ef6-1c3b-4809-a687-4d5d13f343af
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e36b3c6b97fa441297961d2edf889bee61f67cc7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="select-distinct-from-ltmodel-gt-dmx"></a>SELECT DISTINCT FROM&lt;模型&gt;(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回模型中所选列的所有可能状态。 所返回的值会因指定列包含离散值、离散化数值或连续数值而有所变化。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT [FLATTENED] DISTINCT [TOP <n>] <expression list> FROM <model>   
[WHERE <condition list>][ORDER BY <expression>]  
```  
  
## <a name="arguments"></a>参数  
 *n*  
 可选。 一个指定要返回行数的整数。  
  
 *表达式列表*  
 相关列标识符（从模型中派生）或表达式的以逗号分隔的列表。  
  
 *model*  
 一个模型标识符。  
  
 *条件列表*  
 一个限制条件，用于限制从列列表返回的值。  
  
 *expression*  
 可选。 一个返回标量值的表达式。  
  
## <a name="remarks"></a>注释  
 **SELECT DISTINCT FROM**语句只能与单个列或一组相关的列。 该子句不可用于一组不相关的列。  
  
 **SELECT DISTINCT FROM**语句允许您直接引用嵌套表内的列。 例如：  
  
```  
<model>.<table column reference>.<column reference>  
```  
  
 结果**SELECT DISTINCT FROM\<模型 >**语句不同，具体取决于列类型。 下表说明了所支持的列类型和该语句的输出结果。  
  
|列类型|“输出”|  
|-----------------|------------|  
|离散|列中的唯一值。|  
|离散化|列中每个离散化存储桶的中点。|  
|连续|列中各值的中点。|  
  
## <a name="discrete-column-example"></a>离散列示例  
 下面的代码示例基于`[TM Decision Tree]`中创建的模型[Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。 查询返回离散列 `Gender` 中存在的唯一值。  
  
```  
SELECT DISTINCT [Gender]  
FROM [TM Decision Tree]  
```  
  
 示例结果：  
  
|性别|  
|------------|  
||  
|F|  
|M|  
  
 对于包含离散值的列，结果会始终包含 Missing 状态，显示为 Null 值。  
  
## <a name="continuous-column-example"></a>连续列示例  
 以下代码示例返回列中所有值的中点、最小年龄和最大年龄。  
  
```  
SELECT DISTINCT [Age] AS [Midpoint Age],   
    RangeMin([Age]) AS [Minimum Age],   
    RangeMax([Age]) AS [Maximum Age]  
FROM [TM Decision Tree]  
```  
  
 示例结果：  
  
|Midpoint Age|Minimum Age|Maximum Age|  
|------------------|-----------------|-----------------|  
||||  
|62|26|97|  
  
 查询还返回一行表示缺失值的 Null 值。  
  
## <a name="discretized-column-example"></a>离散化列示例  
 下面的代码示例返回算法为 [`Yearly Income]` 列创建的所有存储桶的中点值、最大值和最小值。 若要重新生成此示例的结果，则必须创建一个与 `[Targeted Mailing]` 相同的新挖掘结构。 在向导中，更改的内容类型`Yearly Income`列从**连续**到**Discretized**。  
  
> [!NOTE]  
>  您还可以更改在基础挖掘教程中创建的挖掘模型，以离散化挖掘结构列 [`Yearly Income]`。 有关如何执行此操作的信息，请参阅[更改挖掘模型中的列的离散化](../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)。 但是，当您更改列的离散化时，系统会强制要求重新处理挖掘结构，这将会更改您使用该结构生成的其他模型的结果。  
  
```  
SELECT DISTINCT [Yearly Income] AS [Bucket Average],   
    RangeMin([Yearly Income]) AS [Bucket Minimum],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
 示例结果：  
  
|Bucket Average|Bucket Minimum|Bucket Maximum|  
|--------------------|--------------------|--------------------|  
||||  
|24610.7|10000|39221.41|  
|55115.73|39221.41|71010.05|  
|84821.54|71010.05|98633.04|  
|111633.9|98633.04|124634.7|  
|147317.4|124634.7|170000|  
  
 您可以看到，[Yearly Income] 列的值已经离散化为 5 个存储桶，另外还附加一个 Null 值行，用于表示缺失值。  
  
 结果中小数的位数取决于您用于查询的客户端。 这里已经舍入为两位小数，即简单明了又反映了在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中显示的值。  
  
 例如，如果您使用决策树查看器浏览模型，并单击包含按收入分组的客户的节点，则在工具提示中将显示以下节点属性：  
  
 Age >=69 AND Yearly Income < 39221.41  
  
> [!NOTE]  
>  最小存储桶的最小值和最大存储桶的最大值为所观察到的最高值和最低值。 任何超出此观察范围的值都假定为属于最小存储桶和最大存储桶。  
  
## <a name="see-also"></a>另请参阅  
 [选择 &#40; DMX &#41;](../dmx/select-dmx.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
