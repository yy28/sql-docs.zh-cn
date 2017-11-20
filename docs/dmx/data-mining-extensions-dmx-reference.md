---
title: "数据挖掘扩展插件 (DMX) 引用 |Microsoft 文档"
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
- DMX [Analysis Services]
- statements [DMX]
- Data Mining Extensions [Analysis Services], statements
- DMX [Analysis Services], about Data Mining Extensions
- DMX [Analysis Services], statements
- data definition statements [DMX]
- predictions [DMX]
- Data Mining Extensions [Analysis Services]
- SSAS, DMX
- queries [DMX], extensions reference
- SQL Server Analysis Services, DMX
- OLE DB for Data Mining
- data manipulation statements [DMX]
- Data Mining Extensions [Analysis Services], about Data Mining Extensions
- mining models [Analysis Services], DMX
ms.assetid: 6d85ca20-de67-4e20-b3b5-b734c6cfcece
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4f3c7af23a8013d8c194557bfefaab8a2d4019f4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="data-mining-extensions-dmx-reference"></a>数据挖掘扩展插件 (DMX) 参考
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  数据挖掘扩展插件 (DMX) 是一种可用于创建和使用数据挖掘模型中的语言[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。 可以使用 DMX 创建新数据挖掘模型的结构、为这些模型定型并对其进行浏览、管理和预测。 DMX 由数据定义语言 (DDL) 语句、数据操作语言 (DML) 语句以及函数和运算符组成。  
  
## <a name="microsoft-ole-db-for-data-mining-specification"></a>Microsoft OLE DB for Data Mining 规范  
 中的数据挖掘功能[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]而生成符合[!INCLUDE[msCoName](../includes/msconame-md.md)]OLE DB for Data Mining 规范。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB 数据挖掘规范定义了以下：  
  
-   一种用于保存有关定义数据挖掘模型信息的结构。  
  
-   一种用于创建和处理数据挖掘模型的语言。  
  
 该规范以数据挖掘模型虚拟对象的形式定义数据挖掘的基础。 数据挖掘模型对象将封装所有有关特定挖掘模型的已知内容。 数据挖掘模型对象的结构与 SQL 表类似，包含用于说明模型的列、数据类型和元信息。 该结构允许您使用 DMX 语言（一种 SQL 扩展语言）来创建和处理模型。  
  
 **有关详细信息：** [挖掘结构 &#40;Analysis Services-数据挖掘 &#41;](../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
##  <a name="BKMK_DMXStatements"></a>DMX 语句  
 可以使用 DMX 语句创建、处理、删除、复制、浏览和预测数据挖掘模型。 DMX 中有两种类型的语句：数据定义语句和数据操作语句。 可以使用每种类型的语句执行各种不同的任务。  
  
 有关使用 DMX 语句的详细信息，请参考以下部分的内容：  
  
-   [数据定义语句](#BKMK_DDL)  
  
-   [数据操作语句](#BKMK_DML)  
  
-   [查询基础知识](#BKMK_Queries)  
  
###  <a name="BKMK_DDL"></a>数据定义语句  
 使用 DMX 中的数据定义语句可以创建和定义新的挖掘结构和模型，导入和导出挖掘模型和挖掘结构，以及从数据库中删除现有模型。 DMX 中的数据定义语句属于数据定义语言 (DDL)。  
  
 使用 DMX 中的数据定义语句可以执行下列任务：  
  
-   通过创建挖掘结构[创建挖掘结构](../dmx/create-mining-structure-dmx.md)语句，并通过使用添加到挖掘结构的挖掘模型[ALTER 挖掘结构](../dmx/alter-mining-structure-dmx.md)语句。  
  
-   通过同时创建挖掘模型和关联的挖掘结构[CREATE MINING MODEL](../dmx/create-mining-model-dmx.md)语句以生成空数据挖掘模型对象。  
  
-   挖掘模型和关联的挖掘结构使用导出到文件[导出](../dmx/export-dmx.md)语句。 从由创建 EXPORT 语句使用文件导入挖掘模型和关联的挖掘结构[导入](../dmx/import-dmx.md)语句。  
  
-   将现有挖掘模型的结构复制到新的模型，并使用来训练使用相同的数据， [SELECT INTO](../dmx/select-into-dmx.md)语句。  
  
-   完全使用从数据库删除挖掘模型[DROP MINING MODEL](../dmx/drop-mining-model-dmx.md)语句。 完全挖掘结构及其所有关联的挖掘模型从数据库中删除通过使用[DROP MINING STRUCTURE](../dmx/drop-mining-structure-dmx.md)语句。  
  
 若要了解有关你可以通过使用 DMX 语句执行的数据挖掘任务的详细信息，请参阅[数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)。  
  
 [返回到 DMX 语句](#BKMK_DMXStatements)  
  
###  <a name="BKMK_DML"></a>数据操作语句  
 使用 DMX 中的数据操作语句可以处理现有挖掘模型、浏览模型以及对模型创建预测。 DMX 中的数据操作语句属于数据操作语言 (DML)。  
  
 使用 DMX 中的数据操作语句可以执行下列任务：  
  
-   通过使用定型挖掘模型[INSERT INTO](../dmx/insert-into-dmx.md)语句。 执行该语句不会将实际源数据插入数据挖掘模型对象，但会创建有关说明算法所创建的挖掘模型的摘要信息。 INSERT INTO 语句的源查询述[\<源数据查询 >](../dmx/source-data-query.md)。  
  
-   扩展 SELECT 语句以便浏览在模型定型过程中计算并存储在数据挖掘模型中，例如源数据的统计信息的信息。 以下是可以包括扩展的 SELECT 语句 power 子句：  
  
    -   [SELECT DISTINCT FROM #60; 模型 &#62;&#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md)  
  
    -   [SELECT FROM &#60; 模型 &#62;。内容 &#40; DMX &#41;](../dmx/select-from-model-content-dmx.md)  
  
    -   [SELECT FROM &#60; 模型 &#62;。用例 &#40; DMX &#41;](../dmx/select-from-model-cases-dmx.md)  
  
    -   [SELECT FROM &#60; 模型 &#62;。SAMPLE_CASES &#40; DMX &#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
    -   [SELECT FROM &#60; 模型 &#62;。DIMENSION_CONTENT &#40; DMX &#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
-   创建基于现有挖掘模型使用的预测[PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)子句的 SELECT 语句。 中介绍了 PREDICTION JOIN 语句的源查询[\<源数据查询 >](../dmx/source-data-query.md)。  
  
-   使用从一个模型或结构中删除所有定型的数据[删除 &#40; DMX &#41;](../dmx/delete-dmx.md)语句。  
  
 若要了解有关你可以通过使用 DMX 语句执行的数据挖掘任务的详细信息，请参阅[数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)。  
  
 [返回到 DMX 语句](#BKMK_DMXStatements)  
  
###  <a name="BKMK_Queries"></a>DMX 查询基础知识  
 SELECT 语句是大多数 DMX 查询的基础。 通过将各种子句与此类语句组合使用，可以浏览、复制或预测挖掘模型。 预测查询使用一种形式的选择来创建基于现有挖掘模型的预测。 函数在数据挖掘模型的固有功能的基础上，扩展了您浏览和查询挖掘模型的能力。  
  
 使用 DMX 函数可以获取在模型定型过程中发现的信息，并且还可以计算新的信息。 这些函数可用于多种用途，包括返回说明基础数据或预测精确性的统计信息，或返回预测的详细说明。  
  
 **有关详细信息****信息：** [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)，[常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)，[结构和使用情况的 DMX 预测查询](../dmx/structure-and-usage-of-dmx-prediction-queries.md)，[数据挖掘扩展插件 &#40; DMX &#41;函数参考  ](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
 [返回到 DMX 语句](#BKMK_DMXStatements)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [结构和使用情况的 DMX 预测查询](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  

