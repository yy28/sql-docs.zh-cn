---
title: "数据挖掘架构行集 (SSAs) |Microsoft 文档"
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
ms.topic: article
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- data mining [Analysis Services], queries
- mining model content
- data mining [Analysis Services], schema rowsets
- schema rowsets [Analysis Services], retrieving
- data mining [Analysis Services], troubleshooting
ms.assetid: 442d8c29-07c7-45de-9a15-d556059f68d7
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 23f8b63c593e1269624905caf8809ac5afefd1d5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="data-mining-schema-rowsets-ssas"></a>数据挖掘架构行集 (SSA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，许多现有的 OLE DB 数据挖掘架构行集公开为一组你可以使用查询的数据挖掘扩展插件 (DMX) 语句的系统表。 通过针对数据挖掘架构行集创建查询，可以标识可用的服务，获取您的模型和结构的状态更新，并查找有关模型内容或参数的详细信息。 有关数据挖掘架构行集的说明，请参阅 [Data Mining Schema Rowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)。  
  
> [!NOTE]  
>  还可以使用 XMLA 来查询数据挖掘架构行集。 有关如何在 SQL Server Management Studio 中执行此操作的详细信息，请参阅 [使用 XMLA 创建数据挖掘查询](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md)。  
  
## <a name="list-of-data-mining-schema-rowsets"></a>数据挖掘架构行集列表  
 下表列出了可能对查询和监视有用的数据挖掘架构行集。  
  
|行集名称|Description|  
|-----------------|-----------------|  
|DMSCHEMA_MINING_MODELS|列出了当前上下文中的所有挖掘模型。<br /><br /> 包括诸如创建日期、创建模型时所用的参数以及定型集大小等信息。|  
|DMSCHEMA_MINING_COLUMNS|列出了当前上下文中在挖掘模型中使用的所有列。<br /><br /> 信息包括到挖掘结构源列的映射、数据类型、精度以及可与列一起使用的预测函数。|  
|DMSCHEMA_MINING_STRUCTURES|列出了当前上下文中的所有挖掘结构。<br /><br /> 信息包括结构是否填充、上次处理结构的日期以及结构的维持数据集的定义（如果有）。|  
|DMSCHEMA_MINING_STRUCTURE_COLUMNS|列出了当前上下文中在挖掘结构中使用的所有列。<br /><br /> 信息包括内容类型和数据类型、为 Null 性以及列是否包含嵌套的表数据。|  
|DMSCHEMA_MINING_SERVICES|列出了在指定服务器上可用的所有挖掘服务（或算法）。<br /><br /> 信息包括支持的建模标志、输入类型和支持的数据源类型。|  
|DMSCHEMA_MINING_SERVICE_PARAMETERS|列出了在当前实例上可用的挖掘服务的所有参数。<br /><br /> 信息包括每个参数的数据类型、默认值以及上限和下限。|  
|DMSCHEMA_MODEL_CONTENT|如果模型已处理，则返回模型的内容。<br /><br /> 有关详细信息，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。|  
|DBSCHEMA_CATALOGS|列出了当前 Analysis Services 实例中的所有数据库（目录）。|  
|MDSCHEMA_INPUT_DATASOURCES|列出了当前 Analysis Services 实例中的所有数据源。|  
  
> [!NOTE]  
>  表中的列表不完整；它仅显示针对疑难解答可能最受关注的那些行集。  
  
## <a name="examples"></a>示例  
 下面的部分提供了一些针对数据挖掘架构行集的查询示例。  
  
### <a name="example-1-list-data-mining-services"></a>示例 1：列出数据挖掘服务  
 以下查询返回在当前服务器上可用的挖掘服务（也就是启用的算法）列表。 为每个挖掘服务提供的列包括可由每个算法使用的建模标志和内容类型、每个服务的 GUID，以及可能已为每个服务添加的任何预测限制。  
  
```  
SELECT *  
FROM $system.DMSCHEMA_MINING_SERVICES  
```  
  
### <a name="example-2-list-mining-model-parameters"></a>示例 2：列出挖掘模型参数  
 下面的示例返回创建指定挖掘模型时所使用的参数：  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
### <a name="example-3-list-all-rowsets"></a>示例 3：列出所有行集  
 下面的示例返回在当前服务器上可用的行集的综合性列表：  
  
```  
SELECT *   
FROM $system.DBSCHEMA_TABLES  
```  
  
  
