---
title: DMSCHEMA_MINING_SERVICE_PARAMETERS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 41554600e77c3055f998d7fa32b6f7330c06de52
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="dmschemaminingserviceparameters-rowset"></a>DMSCHEMA_MINING_SERVICE_PARAMETERS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|**SERVICE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**PARAMETER_NAME**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘架构行集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
