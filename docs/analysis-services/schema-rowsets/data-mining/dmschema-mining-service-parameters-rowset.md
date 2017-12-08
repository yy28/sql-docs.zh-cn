---
title: "DMSCHEMA_MINING_SERVICE_PARAMETERS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DMSCHEMA_MINING_SERVICE_PARAMETERS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DMSCHEMA_MINING_SERVICE_PARAMETERS rowset
ms.assetid: 5994e66b-84d0-4279-9f50-d92fd829dd83
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c84d263a312318be40c65c37a168bf11fdc97cfc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="dmschemaminingserviceparameters-rowset"></a>DMSCHEMA_MINING_SERVICE_PARAMETERS 行集
  描述服务器上的算法的参数。  
  
## <a name="rowset-columns"></a>行集列  
 **DMSCHEMA_MINING_SERVICE_PARAMETERS**行集包含以下各列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|算法的名称。|  
|**PARAMETER_NAME**|**DBTYPE_WSTR**|参数名。|  
|**所以**|**DBTYPE_WSTR**|参数的类型。|  
|**IS_REQUIRED**|**DBTYPE_BOOL**|返回一个布尔值**TRUE**如果参数是必需的。|  
|**PARAMETER_FLAGS**|**DBTYPE_UI4**|描述参数特征的位掩码。<br /><br /> **DM_PARAMETER_TRAINING** (**0x0000001**) 指示参数用于定型<br /><br /> **DM_PARAMETER_PREDICTION** (**0x00000002**) 指示参数是否用于预测<br /><br /> **DM_PARAMETER_CONTENT** (**0x00000003**) 指示参数是否用于内容的限制|  
|**DESCRIPTION**|**DBTYPE_WSTR**|参数的用户友好说明。|  
|**默认值**|**DBTYPE_WSTR**|参数的默认值。 返回**NULL**如果默认值不是简单数据类型。|  
|**VALUE_ENUMERATION**|**DBTYPE_WSTR**|参数的可能值的枚举器。|  
|**HELP_FILE**|**DBTYPE_WSTR**|包含此参数文档的文件的名称。|  
|**HELP_CONTEXT**|**DBTYPE_I4**|此函数的帮助上下文 ID。|  
  
## <a name="restriction-columns"></a>限制列  
 **DMSCHEMA_MINING_SERVICE_PARAMETERS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|可选。|  
|**PARAMETER_NAME**|**DBTYPE_WSTR**|可选。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘架构行集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
