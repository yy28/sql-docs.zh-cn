---
title: DMSCHEMA_MINING_STRUCTURES 行集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_STRUCTURES
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURES rowset
ms.assetid: 6224556b-08a0-496e-bd7c-632c3e833e26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 252bd8e96d608314e8030c9bc9e2743df8e23e02
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135977"
---
# <a name="dmschemaminingstructures-rowset"></a>DMSCHEMA_MINING_STRUCTURES 行集
  枚举有关当前目录中的挖掘结构的信息。  
  
## <a name="rowset-columns"></a>行集列  
 `DMSCHEMA_MINING_STRUCTURES`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`||目录名称。|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`||非限定的架构名称。 如果访问接口不支持架构，则为 `NULL`。|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`||结构名称。 此列不能包含 `NULL`。|  
|`STRUCTURE_GUID`|`DBTYPE_GUID`||唯一标识该结构的 GUID 值。 如果访问接口不支持，则为 `NULL`。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||结构的简介。 如果没有与结构相关的说明，则为 `NULL`。|  
|`STRUCTURE_PROPID`|`DBTYPE_UI4`||该结构的属性 ID。 如果访问接口不支持，则为 `NULL`。|  
|`DATE_CREATED`|`DBTYPE_DBTIMESTAMP`||创建结构的日期。 如果访问接口不提供，则为 `NULL`。|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||上次修改结构的日期。 如果访问接口不提供，则为 `NULL`。|  
|`CREATION_STATEMENT`|`DBTYPE_WSTR`||（可选）用于创建原始数据挖掘模型的语句。|  
|`IS_POPULATED`|`DBTYPE_BOOL`||指示结构是否填充的布尔值。<br /><br /> 如果结构已填充，则为 `VARIANT_TRUE`；否则为 `VARIANT_FALSE`。|  
|`LAST_PROCESSED`|`DBTYPE_DBTIMESTAMP`||上次处理结构的日期。 如果访问接口不提供，则为 `NULL`。|  
|`HOLDOUT_MAXPERCENT`|`DBTYPE_ UI1`||用户指定的值，指示作为测试集保持的输入事例的最大百分比。<br /><br /> 0 或 `NULL` 指示没有限制。|  
|`HOLDOUT_MAXCASES`|`DBTYPE_UI8`||用户指定的值，指示作为测试集保留的最大输入事例数。<br /><br /> 0 或 `NULL` 指示没有限制。|  
|`HOLDOUT_SEED`|`DBTYPE_UI8`||用户指定的值，用作可重复分区的种子。<br /><br /> 0 指示将挖掘结构 ID 的哈希用作种子。|  
|`HOLDOUT_ACTUAL_SIZE`|`DBTYPE_UI8`||如果挖掘结构已处理，则此项指示测试数据集的实际大小，以事例数表示。<br /><br /> `NULL` 指示挖掘结构未处理。|  
  
 行集按 `STRUCTURE_CATALOG`、`STRUCTURE_SCHEMA`、`STRUCTURE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制列  
 `DMSCHEMA_MINING_STRUCTURES`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`|可选。|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`|可选。|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘架构行集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
