---
description: 数据挖掘扩展插件 (DMX) 语句参考
title: 数据挖掘扩展插件 (DMX) 语句参考 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ce95adec18bd17dce45fdc988b6db92d66383c74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414093"
---
# <a name="data-mining-extensions-dmx-statements"></a>数据挖掘扩展插件 (DMX) 语句
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  在中使用数据挖掘模型 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 涉及以下主要任务：  
  
-   创建挖掘结构和挖掘模型  
  
-   处理挖掘结构和挖掘模型  
  
-   删除挖掘结构或挖掘模型  
  
-   复制挖掘模型  
  
-   浏览挖掘模型  
  
-   对挖掘模型进行预测  
  
 可以使用数据挖掘扩展插件 (DMX) 语句，以编程方式执行上述每个任务。  
  
 创建挖掘结构和挖掘模型  
 使用 [CREATE 挖掘 structure &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md) 语句将新的挖掘结构添加到数据库中。 然后，您可以使用 [ALTER 挖掘 STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) 语句将挖掘模型添加到挖掘结构中。  
  
 使用 " [创建挖掘模型 &#40;DMX&#41;](../dmx/create-mining-model-dmx.md) 语句来生成新的挖掘模型和关联的挖掘结构。  
  
 处理挖掘结构和挖掘模型  
 使用 [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md) 语句来处理挖掘结构和挖掘模型。  
  
 删除挖掘结构或挖掘模型  
 使用 [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md) 语句从挖掘模型或挖掘结构中删除所有定型的数据。 使用 [DROP 挖掘结构 &#40;dmx&#41;](../dmx/drop-mining-structure-dmx.md) 或 [删除挖掘模型 &#40;dmx&#41;](../dmx/drop-mining-model-dmx.md) 语句，以从数据库中完全删除挖掘结构或挖掘模型。  
  
 复制挖掘模型  
 使用 [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md) 语句将现有挖掘模型的结构复制到新的挖掘模型中，并使用相同的数据为新模型定型。  
  
 浏览挖掘模型  
 使用 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md) 语句来浏览数据挖掘算法在模型定型过程中计算并存储在数据挖掘模型中的信息。 与类似 [!INCLUDE[tsql](../includes/tsql-md.md)] ，可以在 SELECT 语句中使用多个子句来扩展其功能。 这些子句包括[DISTINCT from \<model> ](../dmx/select-distinct-from-model-dmx.md)、 [from \<model> 。事例](../dmx/select-from-model-cases-dmx.md)，[来自 \<model> 。SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md) [ \<model> 。内容](../dmx/select-from-model-content-dmx.md)和[ \<model> 。DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)。  
  
 对挖掘模型进行预测  
 使用 SELECT 语句的 [预测联接](../dmx/select-from-model-prediction-join-dmx.md) 子句来创建基于现有挖掘模型的预测。  
  
 您还可以通过使用 [import &#40;dmx&#41;](../dmx/import-dmx.md) 导入和导出模型，然后将 [&#40;Dmx&#41;语句导出 ](../dmx/export-dmx.md) 。  
  
 上述任务可以分为两类：数据定义语句和数据操作语句，下表对这两类语句进行了说明。  
  
|主题|描述|  
|-----------|-----------------|  
|[数据挖掘扩展插件 (DMX) 数据定义语句](../dmx/dmx-statements-data-definition.md)|数据定义语言 (DDL) 的一部分。 用于定义新挖掘模型（包括定型）或从数据库中删除现有挖掘模型。|  
|[数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)|数据操作语言 (DML) 的一部分。 用于处理现有挖掘模型，包括浏览模型或创建预测。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 语法元素的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
