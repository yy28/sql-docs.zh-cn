---
title: "SELECT FROM&lt;模型&gt;。用例 (DMX) |Microsoft 文档"
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
- SELECT
- CASES
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- SELECT FROM <model>.CASES statement
- drillthrough [DMX]
ms.assetid: d58acb47-aaa6-40b7-b8c4-6a6700fbc1dd
caps.latest.revision: 55
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7f5ec287b2da5998748c19a5000a0a95b658f853
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgtcases-dmx"></a>SELECT FROM&lt;模型&gt;。用例 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  支持钻取功能，并返回用于为模型定型的事例。 如果对挖掘结构和挖掘模型都启用了钻取功能，并且具有相应的权限，则还可以返回未包括在模型中的结构列。  
  
 如果未对挖掘模型启用钻取功能，则此语句将失败。  
  
> [!NOTE]  
>  在数据挖掘扩展插件 (DMX) 中，只能在创建模型时启用钻取功能。 您可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 向现有的模型中添加钻取功能，但是必须先重新处理模型，然后才能查看或查询事例。  
  
 有关如何启用钻取的详细信息，请参阅[创建挖掘模型 &#40; DMX &#41;](../dmx/create-mining-model-dmx.md)， [SELECT INTO &#40; DMX &#41;](../dmx/select-into-dmx.md)，和[ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>参数  
 *n*  
 選擇性。 一个指定返回行数的整数。  
  
 *表达式列表*  
 一个逗号分隔的表达式列表。 该表达式可以包括列标识符、用户定义函数、UDF 以及 VBA 函数等。  
  
 若要包括挖掘模型中没有包括的结构列，请使用函数 `StructureColumn('<structure column name>')`。  
  
 *model*  
 一个模型标识符。  
  
 *条件表达式*  
 一个限制条件，用于限制从列列表返回的值。  
  
 *expression*  
 選擇性。 一个返回标量值的表达式。  
  
## <a name="remarks"></a>注释  
 如果对挖掘模型和挖掘结构都启用了钻取功能，那么作为具有模型和结构钻取权限的角色成员的用户，可以访问没有包括在挖掘模型中的挖掘结构列。 因此，为了保护敏感数据或个人信息，你应该构建你的数据源视图来屏蔽个人信息，并授予**AllowDrillthrough**必要时的挖掘结构权限。  
  
 [延隔时间 &#40; DMX &#41;](../dmx/lag-dmx.md)函数可与时序模型返回或筛选每个用例和初始时间之间的时间间隔。  
  
 使用[IsInNode &#40; DMX &#41;](../dmx/isinnode-dmx.md)函数中**其中**子句将返回架构行集的 NODE_UNIQUE_NAME 列指定的节点与相关联的情况。  
  
## <a name="examples"></a>示例  
 下面的示例基于挖掘结构目标邮递，基于[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]数据库和其关联的挖掘模型。 有关详细信息，请参阅[Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。  
  
### <a name="example-1-drillthrough-to-model-cases-and-structure-columns"></a>示例 1：钻取到模型事例和结构列  
 以下示例返回用于测试目标邮件模型的所有事例的列。 如果建立模型所依据的挖掘结构不存在维持测试数据集，此查询将返回 0 个事例。 可以使用表达式列表仅返回需要的列。  
  
```  
SELECT * FROM [TM Decision Tree].Cases  
WHERE IsTestCase();  
```  
  
### <a name="example-2-drillthrough-to-training-cases-in-a-specific-node"></a>示例 2：钻取到特定节点中的定型事例  
 以下示例只返回那些用于对分类 2 进行定型的事例。 分类 2 节点的 NODE_UNIQUE_NAME 列的值为“002”。 该示例还将返回一个不作为挖掘模型组成部分的结构列 [Customer Key]，并为该列提供别名 `CustomerID`。 请注意，结构列的名称作为字符串值传递，因此必须用引号引起来，而不是用括号括起来。  
  
```  
SELECT StructureColumn('Customer Key') AS CustomerID, *   
FROM [TM_Clustering].Cases  
WHERE IsTrainingCase()  
AND IsInNode('002')  
```  
  
 若要返回结构列，必须对挖掘模型和挖掘结构都启用钻取权限。  
  
> [!NOTE]  
>  并非所有挖掘模型类型都支持钻取功能。 有关支持钻取的模型的信息，请参阅[钻取查询 &#40; 数据挖掘 &#41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
## <a name="see-also"></a>另请参阅  
 [选择 &#40; DMX &#41;](../dmx/select-dmx.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

