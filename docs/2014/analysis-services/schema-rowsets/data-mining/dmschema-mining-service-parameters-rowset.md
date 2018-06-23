---
title: DMSCHEMA_MINING_SERVICE_PARAMETERS 行集 |Microsoft 文档
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
- DMSCHEMA_MINING_SERVICE_PARAMETERS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICE_PARAMETERS rowset
ms.assetid: 5994e66b-84d0-4279-9f50-d92fd829dd83
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9079be52d50da3a400496dc602166c857f2b1691
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125711"
---
# <a name="dmschemaminingserviceparameters-rowset"></a>DMSCHEMA_MINING_SERVICE_PARAMETERS 行集
  描述服务器上的算法的参数。  
  
## <a name="rowset-columns"></a>行集列  
 `DMSCHEMA_MINING_SERVICE_PARAMETERS`行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||算法的名称。|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`||参数名。|  
|`PARAMETER_TYPE`|`DBTYPE_WSTR`||参数的类型。|  
|`IS_REQUIRED`|`DBTYPE_BOOL`||一个布尔值，如果参数是必需的，则返回 `TRUE`。|  
|`PARAMETER_FLAGS`|`DBTYPE_UI4`||描述参数特征的位掩码。<br /><br /> -   `DM_PARAMETER_TRAINING` (`0x0000001`) 指示参数用于定型<br />-   `DM_PARAMETER_PREDICTION` (`0x00000002`) 指示参数是否用于预测<br />-   `DM_PARAMETER_CONTENT` (`0x00000003`) 指示参数是否用于内容的限制|  
|`DESCRIPTION`|`DBTYPE_WSTR`||参数的用户友好说明。|  
|`DEFAULT_VALUE`|`DBTYPE_WSTR`||参数的默认值。 如果默认值不是简单数据类型，则返回 `NULL`。|  
|`VALUE_ENUMERATION`|`DBTYPE_WSTR`||参数的可能值的枚举器。|  
|`HELP_FILE`|`DBTYPE_WSTR`||包含此参数文档的文件的名称。|  
|`HELP_CONTEXT`|`DBTYPE_I4`||此函数的帮助上下文 ID。|  
  
## <a name="restriction-columns"></a>限制列  
 `DMSCHEMA_MINING_SERVICE_PARAMETERS`行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|可选。|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘架构行集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  