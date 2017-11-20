---
title: "&lt;源数据查询&gt;|Microsoft 文档"
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
- data sources [DMX]
- predictions [DMX]
- source data query element
- queries [DMX], source data
- external data access [DMX]
- <source data query> element
- training mining models
ms.assetid: 9dce5e37-1354-4d28-87c2-f9c419cb5b09
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 195c2ecd04a28ad830aca2d90df821b76d46e98e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="ltsource-data-querygt"></a>&lt;源数据查询&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  若要训练数据挖掘模型，并从挖掘模型创建预测，你必须访问外部的数据[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库。 你使用\<源数据查询 > 子句在数据挖掘扩展插件 (DMX) 来定义此外部数据。 [INSERT INTO &#40; DMX &#41;](../dmx/insert-into-dmx.md)， [SELECT FROM #60; 模型 &#62;预测联接 &#40; DMX &#41;](../dmx/select-from-model-prediction-join-dmx.md)，和[选择从 NATURAL PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)语句所有使用**\<源数据查询 >**。  
  
## <a name="query-types"></a>查询类型  
 指定源数据最常用的三种方式包括：  
  
 [OPENQUERY &#40; DMX &#41;](../dmx/source-data-query-openquery.md)  
 通过使用现有数据源，此语句可查询 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例以外的数据。  
  
 虽然**OPENQUERY**在功能上与类似**OPENROWSET**， **OPENQUERY**具有以下优点：  
  
-   DMX 查询是更易于编写与**OPENQUERY**。 您可以利用数据源中现有的连接字符串，而无需在每次编写查询时都创建一个新的连接字符串。 数据源对象还可以控制各个用户对数据的访问。  
  
-   管理员可以更好地控制对服务器上数据的访问方式。 例如，管理员可以管理哪些提供程序可以载入服务器以及可以访问哪些外部数据。  
  
 [OPENROWSET &#40; DMX &#41;](../dmx/source-data-query-openrowset.md)  
 通过使用现有数据源，此语句可查询 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例以外的数据。  
  
 [形状 &#40; DMX &#41;](../dmx/source-data-query-shape.md)  
 此语句可以查询多个数据源以创建嵌套表。 通过使用**形状**，可以将来自多个源的数据合并到单个层次结构表。 这样便可利用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的功能，通过在表中嵌入表的方式来嵌套表。  
  
 若要指定源数据，还可以使用下列选项：  
  
-   任何有效的 DMX 语句  
  
-   任何有效的多维表达式 (MDX) 语句  
  
-   返回存储过程的表  
  
-   XML for Analysis (XMLA) 行集  
  
-   行集参数  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [嵌套的表 &#40;Analysis Services-数据挖掘 &#41;](../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
  

