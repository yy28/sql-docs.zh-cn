---
title: 查询数据挖掘架构行集 (Analysis Services-数据挖掘) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- data mining [Analysis Services], queries
- mining model content
- data mining [Analysis Services], schema rowsets
- schema rowsets [Analysis Services], retrieving
- data mining [Analysis Services], troubleshooting
ms.assetid: 442d8c29-07c7-45de-9a15-d556059f68d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30a4a503b16693a3774aa7f68771fb0f9dd70810
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66084911"
---
# <a name="querying-the-data-mining-schema-rowsets-analysis-services---data-mining"></a>查询数据挖掘架构行集（Analysis Services - 数据挖掘）
  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，许多现有 OLE DB 数据挖掘架构行集已作为可以使用数据挖掘扩展插件 (DMX) 语句轻松查询的一组系统表公开。 通过针对数据挖掘架构行集创建查询，可以标识可用的服务，获取您的模型和结构的状态更新，并查找有关模型内容或参数的详细信息。 有关数据挖掘架构行集的说明，请参阅 [Data Mining Schema Rowsets](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
> [!NOTE]  
>  还可以使用 XMLA 来查询数据挖掘架构行集。 有关如何在 SQL Server Management Studio 中执行此操作的详细信息，请参阅 [使用 XMLA 创建数据挖掘查询](create-a-data-mining-query-by-using-xmla.md)。  
  
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
|DMSCHEMA_MODEL_CONTENT|如果模型已处理，则返回模型的内容。<br /><br /> 有关详细信息，请参阅[挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)。|  
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
  
### <a name="example-3-list-all-rowsets"></a>示例 3:列出所有行集  
 下面的示例返回在当前服务器上可用的行集的综合性列表：  
  
```  
SELECT *   
FROM $system.DBSCHEMA_TABLES  
```  
  
## <a name="see-also"></a>请参阅  
 [故障排除概念 (Analysis Services-数据挖掘)](https://msdn.microsoft.com/library/cc645881.aspx)  
  
  
