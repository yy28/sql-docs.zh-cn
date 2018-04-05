---
title: DISCOVER_KEYWORDS 行集 (XMLA) |Microsoft 文档
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
- DISCOVER_KEYWORDS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_KEYWORDS rowset
ms.assetid: 99945e53-3a1b-4d7b-9aff-712977db8b2d
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0529692c18cb33848bf74bd7ed2c2e64dcdebe74
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="discoverkeywords-rowset-xmla"></a>DISCOVER_KEYWORDS 行集 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]返回有关保留的关键字的信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)]XML for Analysis (XMLA) 提供。  
  
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
  
  
