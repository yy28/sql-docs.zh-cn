---
title: DMSCHEMA_MINING_MODELS 行集 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_MODELS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_MODELS rowset
ms.assetid: 1636f4cf-b342-4e2e-93b4-04136e2d41ef
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d8296ddb800b7691936236aa0cdb6550c89c34c2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124202"
---
# <a name="dmschemaminingmodels-rowset"></a>DMSCHEMA_MINING_MODELS 行集
  枚举当前目录中的数据挖掘模型。 `DMSCHEMA_MINING_MODELS` 行集包含与每个挖掘模型关联的信息，如模型名称、处理日期和挖掘算法。  
  
 实例时都提供 SQL Server 登录名。 `DMSCHEMA_MINING_MODELS`架构行集是非常类似于[DBSCHEMA_TABLES](../ole-db/dbschema-tables-rowset.md)架构行集，并且可以用于相同的方式。  
  
## <a name="rowset-columns"></a>行集列  
 `DMSCHEMA_MINING_MODELS`行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||目录名称。 使用模型为其成员的数据库的名称填充。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||非限定的架构名称。 此列不支持通过[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含`NULL`。|  
|`MODEL_NAME`|`DBTYPE_WSTR`||挖掘模型名称。 此列包含挖掘模型的名称，并且永远不为空。|  
|`MODEL_TYPE`|`DBTYPE_WSTR`||模型类型。|  
|`MODEL_GUID`|`DBTYPE_GUID`||模型的 GUID。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||模型的用户友好说明。|  
|`MODEL_PROPID`|`DBTYPE_UI4`||模型的属性 ID。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支持此列；该列始终包含 `NULL`。|  
|`DATE_CREATED`|`DBTYPE_DBTIMESTAMP`||创建模型的日期。|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||上次修改模型定义的日期。|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`||标识模型使用的数据挖掘算法类型的枚举。 此类型可以是下列值之一：<br /><br /> -   `DM_SERVICETYPE_CLASSIFICATION` (1)<br />-   `DM_SERVICETYPE_SEGMENTATION`(2)<br />-   `DM_SERVICETYPE_ ASSOCIATION`(4)<br />-   `DM_SERVICETYPE_ DENSITY_ESTIMATE`(8)<br />-   `DM_SERVICETYPE_SEQUENCE`(16)|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||模型使用的数据挖掘算法的特定于访问接口的名称。|  
|`CREATION_STATEMENT`|`DBTYPE_WSTR`||用于创建挖掘模型的语句。|  
|`PREDICTION_ENTITY`|`DBTYPE_WSTR`||指示可预测的挖掘列的逗号分隔列表。|  
|`IS_POPULATED`|`DBTYPE_BOOL`||指示模型是否填充的布尔型标志。<br /><br /> 如果填充该模型，则为 `TRUE`；否则为 `FALSE`。|  
|`MINING_PARAMETERS`|`DBTYPE_WSTR`||创建模型时使用的参数的逗号分隔的列表。|  
|`MINING_STRUCTURE`|`DBTYPE_WSTR`||模型所基于的挖掘结构的 ID。|  
|`LAST_PROCESSED`|`DBTYPE_DBTIMESTAMP`||上次处理模型的日期。|  
|`MSOLAP_IS_DRILLTHROUGH_ENABLED`|`DBTYPE_BOOL`||指示模型是否支持钻取的布尔型标志。|  
|`FILTER`|`DBTYPE_WSTR`||与挖掘模型关联的筛选表达式。<br /><br /> NULL 或空字符串指示不应用筛选器。|  
|`TRAINING_SET_SIZE`|`DBTYPE_UIS`||包含在设置处理结构后之后的任何筛选器应用于模型, 的挖掘模型定型的事例数。|  
  
## <a name="restriction-columns"></a>限制列  
 可以使用以下表中的列对 `DMSCHEMA_MINING_MODELS` 行集进行限制。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|可选。|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|可选。|  
|`MODEL_NAME`|`DBTYPE_WSTR`|可选。|  
|`MODEL_TYPE`|`DBTYPE_WSTR`|可选。|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|可选。|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`|可选。|  
|`MINING_STRUCTURE`|`DBTYPE_WSTR`|可选。|  
  
 有关如何查询此行集的示例，请参阅[查询参数用来创建挖掘模型](../../data-mining/query-the-parameters-used-to-create-a-mining-model.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘架构行集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  