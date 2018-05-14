---
title: DMSCHEMA_MINING_MODEL_XML 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e4aa4451c8fed5ceec07609bbb0a22628bc35777
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="dmschemaminingmodelxml-rowset"></a>DMSCHEMA_MINING_MODEL_XML 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  返回挖掘模型的 XML 结构。 该 XML 字符串的格式遵循预测模型标记语言 (PMML 2.1) 标准。  
  
## <a name="rowset-columns"></a>行集列  
 **DMSCHEMA_MINING_MODEL_XML**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||目录名称。 使用模型为其成员的数据库的名称填充。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||非限定的架构名称。 此列不支持通过[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它始终包含**NULL**。|  
|**MODEL_NAME**|**DBTYPE_WSTR**||模型名称。 此列不能包含**NULL**。|  
|**MODEL_TYPE**|**DBTYPE_WSTR**||模型类型。 它是特定于访问接口的字符串。 它可以是**NULL**。|  
|**MODEL_GUID**|**DBTYPE_GUID**||标识模型的 GUID。 提供程序并使用 Guid 来标识表返回**NULL**。|  
|**MODEL_PMML**|**DBTYPE_WSTR**||以 PMML 格式表示的模型内容的 XML 表示形式。|  
|**SIZE**|**DBTYPE_UI4**||XML 字符串中的字节数。|  
|**位置**|**DBTYPE_WSTR**||XML 文件的位置。 它是**NULL**如果物理文件不用于存储。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 对于 DMSCHEMA_MINING_MODEL_XML 行集，可对下表中列出的列进行限制。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_W**STR|選擇性。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘架构行集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
