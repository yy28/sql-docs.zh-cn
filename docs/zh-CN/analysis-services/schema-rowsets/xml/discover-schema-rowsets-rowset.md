---
title: DISCOVER_SCHEMA_ROWSETS 行集 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DISCOVER_SCHEMA_ROWSETS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_SCHEMA_ROWSETS rowset
ms.assetid: e5012aa0-6ef8-497f-96c1-2772e2394f62
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fafe6ed5d5a81cb73ddc53a68408e4548ac92699
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="discoverschemarowsets-rowset"></a>DISCOVER_SCHEMA_ROWSETS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  返回 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口支持的所有枚举值以及任何其他特定于访问接口的枚举值的名称、限制、说明以及其他信息。  
  
 如果调用[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法替换**DISCOVER_SCHEMA_ROWSETS**中的枚举值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)元素，**发现**方法返回**DISCOVER_SCHEMA_ROWSETS**行集。  
  
## <a name="rowset-columns"></a>行集列  
 DISCOVER_SCHEMA_ROWSETS 行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**schemaName**|**DBTYPE_WSTR**||架构或请求的名称。 此请求返回中的值*RequestTypes*枚举。|  
|**SchemaGuid**|**DBTYPE_GUID**||架构的 GUID。|  
|**限制**|**DBTYPE_HCHAPTER**||受访问接口支持的一组限制。|  
|**Description**|**DBTYPE_WSTR**||架构的可本地化说明。|  
|**RestrictionsMask**|**DBTYPE_UI8**|||  
  
 未对此架构行集进行排序。  
  
 提供程序为 DBSCHEMA_MEMBERS 架构行集，支持的三个限制**限制**数组可能会返回以下结果。 结果中的元素会引用架构中的列名。  
  
```  
<Restrictions>  
      <CATALOG_NAME type="string" />   
      <SCHEMA_NAME type="string" />   
      <CUBE_NAME type="string" />   
</Restrictions>  
```  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_SCHEMA_ROWSETS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**schemaName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
