---
title: DISCOVER_LITERALS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ed865f22291b3e2e47c4934e455e0e75795d35cc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="discoverliterals-rowset"></a>DISCOVER_LITERALS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  返回有关 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口支持的文字的信息，包括数据类型和值。  
  
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
|**LiteralName**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_KEYWORDS 行集 & #40;XMLA & #41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)  
  
  
