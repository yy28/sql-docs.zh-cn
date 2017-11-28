---
title: "DISCOVER_KEYWORDS 行集 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DISCOVER_KEYWORDS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_KEYWORDS rowset
ms.assetid: 99945e53-3a1b-4d7b-9aff-712977db8b2d
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a3b07baa51b0b7dbfcdbb41a782fe4a4cab2f2cd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="discoverkeywords-rowset-xmla"></a>DISCOVER_KEYWORDS 行集 (XMLA)
  返回 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口保留的关键字的相关信息。  
  
 如果调用[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法替换**DISCOVER_KEYWORDS**中的枚举值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)元素，**发现**方法返回**DISCOVER_KEYWORDS**行集。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_KEYWORDS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**关键字**|**DBTYPE_WSTR**||访问接口保留的所有关键字的列表。<br /><br /> 示例： **AND**|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_KEYWORDS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**关键字**|**DBTYPE_WSTR**|可选。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_LITERALS 行集](../../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)  
  
  
