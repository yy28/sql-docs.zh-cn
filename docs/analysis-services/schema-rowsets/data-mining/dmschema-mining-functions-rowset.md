---
title: DMSCHEMA_MINING_FUNCTIONS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f92a3028f9397283f8d5820c54d823e40b8fdc3d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="dmschemaminingfunctions-rowset"></a>DMSCHEMA_MINING_FUNCTIONS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  介绍可在正在运行的服务器上的数据挖掘算法支持的数据挖掘函数[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="rowset-columns"></a>行集列  
 **DMSCHEMA_MINING_FUNCTIONS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**||算法的名称。|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**||函数的名称。|  
|**FUNCTION_SIGNATURE**|**DBTYPE_WSTR**||函数的签名。|  
|**RETURNS_TABLE**|**DBTYPE_BOOL**||**FALSE**如果该函数将返回标量内容 （如字符自变量的长度中）;**TRUE**如果函数返回一个表 （如一个直方图表中）。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||函数的用户友好说明。|  
|**HELP_FILE**|**DBTYPE_WSTR**||包含此函数文档的文件的名称。|  
|**HELP_CONTEXT**|**DBTYPE_I4**||此函数的帮助上下文 ID。|  
  
## <a name="restriction-columns"></a>限制列  
 **DMSCHEMA_MINING_FUNCTIONS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘架构行集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
