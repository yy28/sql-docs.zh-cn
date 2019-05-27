---
title: 建模标志 （数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- data types [data mining]
- REGRESSOR flag
- MODEL_EXISTENCE_ONLY flag
- REGRESSOR column
- columns [data mining], modeling flags
- NOT NULL modeling flag
- modeling flags [data mining]
- null values [Analysis Services]
- MODEL_EXISTENCE_ONLY column
- coding [Data Mining]
ms.assetid: 8826d5ce-9ba8-4490-981b-39690ace40a4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 37263c42e4e9f37b1b782dc07b8df03f77092b14
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083312"
---
# <a name="modeling-flags-data-mining"></a>建模标志（数据挖掘）
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，可以使用建模标志为数据挖掘算法提供有关事例表中定义的数据的附加信息。 该算法可以使用该附加信息生成更精确的数据挖掘模型。  
  
 某些建模标志是在挖掘结构级别定义的，而其他标志则是在挖掘模型列级别定义的。 例如，可以将 `NOT NULL` 建模标志与挖掘结构列一起使用。 您可以根据用于创建模型的算法，在挖掘模型列上定义其他建模标志。  
  
> [!NOTE]  
>  除了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]预定义的这些标志以外，第三方插件还可能具有其他建模标志。  
  
## <a name="list-of-modeling-flags"></a>建模标志列表  
 下面的列表介绍了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中支持的建模标志。 有关特定算法支持的建模标志的信息，请参阅用于创建模型的算法的技术参考主题。  
  
 `NOT NULL`  
 指示属性列的值不应包含 Null 值。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在模型定型过程中发现该属性列的值为 Null 值，则将出现错误。  
  
 **MODEL_EXISTENCE_ONLY**  
 指示该列将被视为具有两种状态：`Missing` 和 `Existing`。 如果该值为 `NULL`，将被视为 Missing。 MODEL_EXISTENCE_ONLY 标志将应用于可预测属性，并且大多数算法都支持该标志。  
  
 实际上，将 MODEL_EXISTENCE_ONLY 标志设置为 `True` 会更改值的表示形式，以使得仅存在两种状态：`Missing` 和 `Existing`。 将所有非 Missing 状态合并为一个 `Existing` 值。  
  
 此建模标志的典型用法是指示以下情况中的属性：`NULL` 状态具有隐含意义；`NOT NULL` 状态的显式值可能不与列中有任意值时一样重要。 例如，如果某个合同永远不会签署，则 [DateContractSigned] 列可能为 `NULL`，但如果该合同已签署，则 [DateContractSigned] 列为 `NOT NULL`。 因此，如果模型的目的是用于预测合同是否会签署，则可以使用 MODEL_EXISTENCE_ONLY 标志忽略 `NOT NULL` 事例中的准确日期值，而只区分联系人为 `Missing` 或 `Existing` 的事例。  
  
> [!NOTE]  
>  Missing 是算法所使用的一种特殊状态，不同于列中文本值 “Missing”。 有关详细信息，请参阅 [缺失值（Analysis Services - 数据挖掘）](missing-values-analysis-services-data-mining.md)预定义的这些标志以外，第三方插件还可能具有其他建模标志。  
  
 `REGRESSOR`  
 指示该列在处理期间适合用作回归量。 该标志是在挖掘模型列中定义的，只能将其应用于具有连续数值数据类型的列。 有关使用此标志的详细信息，请参阅本主题中的 [使用 REGRESSOR 建模标志](#bkmk_UseRegressors)这一部分。  
  
## <a name="viewing-and-changing-modeling-flags"></a>查看和更改建模标志  
 通过查看结构或模型的属性，可以在数据挖掘设计器中查看与挖掘结构列或模型列关联的建模标志。  
  
 若要确定已应用于当前挖掘结构的建模标志，可使用与如下查询创建一个针对数据挖掘架构行集的查询，用于仅返回结构列的建模标志：  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_STRUCTURE_COLUMNS  
WHERE STRUCTURE_NAME = '<structure name>'  
```  
  
 可通过使用数据挖掘设计器并编辑关联列的属性，来添加或更改模型中使用的建模标志。 此类更改需要重新处理结构或模型。  
  
 可使用 DMX 或使用 AMO 或 XMLA 脚本来指定新挖掘结构或挖掘模型中的建模标志。 但是，不能使用 DMX 更改现有挖掘模型和结构中使用的建模标志。 您必须使用语法 `ALTER MINING STRUCTURE....ADD MINING MODEL`创建新的挖掘模型。  
  
##  <a name="bkmk_UseRegressors"></a> 使用 REGRESSOR 建模标志  
 当对某个列设置 REGRESSOR 建模标志时，指示的是列包含潜在回归量的算法。 模型中使用的实际回归量是由算法确定的。 如果潜在回归量不对可预测属性建模，则可以忽略该潜在回归量。  
  
 使用数据挖掘向导构建模型时，会将所有的连续输入列都标记为潜在回归量。 因此，即使没有为某个列显式设置 REGRESSOR 标记，该列也可能会在模型中用作回归量。  
  
 您可以通过对挖掘模型的架构行集执行查询来确定处理的模型中实际使用的回归量，如下面的示例所示：  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_COLUMNS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 **注意** 如果修改某个挖掘模型并将某列的内容类型从连续更改为离散，则必须手动更改该挖掘列上的标志，然后重新处理该模型。  
  
### <a name="regressors-in-linear-regression-models"></a>线性回归模型中的回归量  
 线性回归模型基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法。 即使不使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法，任何决策树模型也都可以包含表示连续属性的回归的树或节点。  
  
 因此，在这些模型中，您无需指定连续列表示回归量。 即使不对列设置 REGRESSOR 标志， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法也会将数据集分区成具有有意义模式的区域。 其差异是：如果设置建模标志，此算法将尝试查找以下形式的回归等式，以适合树中节点的模式。  
  
 a*C1 + b\*C2 + ...  
  
 然后，将对剩余的总和进行计算，如果偏差过大，则在树中执行强制拆分。  
  
 例如，如果是将 **Income** 用作属性来预测客户购买行为，并对该列设置了 REGRESSOR 建模标志，则该算法将使用标准回归公式先尝试适合 **Income** 值。 如果偏差过大，则放弃使用回归公式，并根据其他一些属性对树进行拆分。 拆分后，该决策树算法随后尝试适合每个分支中收入的回归量。  
  
 可以使用 FORCE_REGRESSOR 参数来保证该算法使用特定的回归量。 此参数可以与决策树算法和线性回归算法一起使用。  
  
## <a name="related-tasks"></a>Related Tasks  
 使用以下链接了解有关使用建模标志的详细信息。  
  
|任务|主题|  
|----------|-----------|  
|使用数据挖掘设计器编辑建模标志|[查看或更改建模标志（数据挖掘）](modeling-flags-data-mining.md)|  
|指定算法的提示以建议可能的回归量|[在模型中指定用作回归量的列](specify-a-column-to-use-as-regressor-in-a-model.md)|  
|请参阅特定算法支持的建模标志（在每个算法参考主题的“建模标志”部分中）|[数据挖掘算法（Analysis Services - 数据挖掘）](data-mining-algorithms-analysis-services-data-mining.md)|  
|了解有关挖掘结构列以及可对其设置的属性的更多信息|[挖掘结构列](mining-structure-columns.md)|  
|了解可在模型级别应用的挖掘模型列和建模标志|[挖掘模型列](mining-model-columns.md)|  
|请参阅用于在 DMX 语句中使用建模标志的语法|[建模标志 (DMX)](/sql/dmx/modeling-flags-dmx)|  
|了解缺失值以及如何处理它们|[缺失值（Analysis Services - 数据挖掘）](missing-values-analysis-services-data-mining.md)|  
|了解如何管理模型和结构以及设置用法属性|[移动数据挖掘对象](moving-data-mining-objects.md)|  
  
  
