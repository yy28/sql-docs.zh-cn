---
title: "DISCOVER_LITERALS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DISCOVER_LITERALS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_LITERALS rowset
ms.assetid: 1bf0a2e2-a419-4c25-b271-37dfa44de2ea
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ae4dfbe2c5f7d9ce9281dd483b7544fb358dd1df
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="discoverliterals-rowset"></a>DISCOVER_LITERALS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]返回包括数据类型和支持的值的文字信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)]XML for Analysis (XMLA) 提供。  
  
 如果调用[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法替换**DISCOVER_LITERALS**中的枚举值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)元素，**发现**方法返回**DISCOVER_LITERALS**行集。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_LITERALS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**LiteralName**|**DBTYPE_WSTR**||在行中说明的文字的名称。<br /><br /> 例如： **DBLITERAL_LIKE_PERCENT**|  
|**LiteralValue**|**DBTYPE_WSTR**||实际文字值。<br /><br /> 例如，如果**LiteralName**是**DBLITERAL_LIKE_PERCENT**和的百分比字符 (**%**) 与 LIKE 子句，值中的零个或多个字符匹配**LiteralValue**列为"**%**"。|  
|**LiteralInvalidChars**|**DBTYPE_WSTR**||文字中的无效字符。<br /><br /> 例如，如果表名称只能包含数字字符之外的任何内容，此字符串是"**0123456789**"。|  
|**LiteralInvalidStartingChars**|**DBTYPE_WSTR**||当用作文字的第一个字符时无效的字符。 如果文本可以从任何有效的字符开始，这是**null**。|  
|**LiteralMaxLength**|**DBTYPE_I4**||文字中的最大字符数。 如果没有最大值或最大值未知，则该值为 –1。|  
|**LiteralNameEnumValue**|**DBTYPE_I4**|||  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_LITERALS**行集可限制下表中的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**LiteralName**|**DBTYPE_WSTR**|可选。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_KEYWORDS 行集 &#40;XMLA &#41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)  
  
  
