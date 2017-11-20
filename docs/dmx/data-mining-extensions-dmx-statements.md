---
title: "数据挖掘扩展插件 (DMX) 语句引用 |Microsoft 文档"
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
dev_langs:
- DMX
helpviewer_keywords:
- Data Mining Extensions [Analysis Services], statements
- DMX [Analysis Services], statements
- statements [DMX], reference
- mining models [Analysis Services], training
- mining structures [DMX]
- mining models [Analysis Services], options
- mining structures [DMX], options
ms.assetid: 9cfa1db4-0f21-4fa3-8158-f94c48987e1b
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e7c9740eebec925bc2b25c6437f488f898288a1e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="data-mining-extensions-dmx-statements"></a>数据挖掘扩展插件 (DMX) 语句
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在数据挖掘模型中使用[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]涉及以下主要任务：  
  
-   创建挖掘结构和挖掘模型  
  
-   处理挖掘结构和挖掘模型  
  
-   删除挖掘结构或挖掘模型  
  
-   复制挖掘模型  
  
-   浏览挖掘模型  
  
-   对挖掘模型进行预测  
  
 可以使用数据挖掘扩展插件 (DMX) 语句，以编程方式执行上述每个任务。  
  
 创建挖掘结构和挖掘模型  
 使用[创建挖掘结构 &#40; DMX &#41;](../dmx/create-mining-structure-dmx.md)语句向数据库添加新的挖掘结构。 然后，可以使用[ALTER 挖掘结构 &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md)语句将挖掘模型添加到挖掘结构。  
  
 使用[CREATE MINING MODEL &#40; DMX &#41;](../dmx/create-mining-model-dmx.md)语句以生成新的挖掘模型和关联的挖掘结构。  
  
 处理挖掘结构和挖掘模型  
 使用[INSERT INTO &#40; DMX &#41;](../dmx/insert-into-dmx.md)语句来处理挖掘结构和挖掘模型。  
  
 删除挖掘结构或挖掘模型  
 使用[删除 &#40; DMX &#41;](../dmx/delete-dmx.md)语句以从挖掘模型或挖掘结构中删除所有定型的数据。 使用[删除挖掘结构 &#40; DMX &#41;](../dmx/drop-mining-structure-dmx.md)或[DROP MINING MODEL &#40; DMX &#41;](../dmx/drop-mining-model-dmx.md)语句以从数据库中完全删除挖掘结构或挖掘模型。  
  
 复制挖掘模型  
 使用[SELECT INTO &#40; DMX &#41;](../dmx/select-into-dmx.md)语句以将现有的挖掘模型的结构复制到新的挖掘模型并使用相同的数据为新模型定型。  
  
 浏览挖掘模型  
 使用[选择 &#40; DMX &#41;](../dmx/select-dmx.md)语句来浏览数据挖掘算法计算并在模型定型过程将存储在数据挖掘模型的信息。 与相似与[!INCLUDE[tsql](../includes/tsql-md.md)]，你可以使用多个子句的 SELECT 语句，扩展其 power。 这些子句包括[不同从\<模型 >](../dmx/select-distinct-from-model-dmx.md)， [FROM\<模型 >。用例](../dmx/select-from-model-cases-dmx.md)， [FROM\<模型 >。SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)， [FROM\<模型 >。内容](../dmx/select-from-model-content-dmx.md)和[FROM\<模型 >。DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)。  
  
 对挖掘模型进行预测  
 使用[PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)子句的 SELECT 语句以创建基于现有挖掘模型的预测。  
  
 你也可以导入和导出模型通过使用[导入 &#40; DMX &#41;](../dmx/import-dmx.md)和[导出 &#40; DMX &#41;](../dmx/export-dmx.md)语句。  
  
 上述任务可以分为两类：数据定义语句和数据操作语句，下表对这两类语句进行了说明。  
  
|主题|Description|  
|-----------|-----------------|  
|[数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)|数据定义语言 (DDL) 的一部分。 用于定义新挖掘模型（包括定型）或从数据库中删除现有挖掘模型。|  
|[数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)|数据操作语言 (DML) 的一部分。 用于处理现有挖掘模型，包括浏览模型或创建预测。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  

