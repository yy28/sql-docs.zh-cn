---
title: DISCOVER_LITERALS 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DISCOVER_LITERALS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_LITERALS rowset
ms.assetid: 1bf0a2e2-a419-4c25-b271-37dfa44de2ea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e218c03cd6d2f8dbf06501dd18a2c4c3e4977eca
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063207"
---
# <a name="discoverliterals-rowset"></a>DISCOVER_LITERALS 行集
  返回有关 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口支持的文字的信息，包括数据类型和值。  
  
 如果您调用[Discover](../../xmla/xml-elements-methods-discover.md)方法替换`DISCOVER_LITERALS`中的枚举值[RequestType](../../xmla/xml-elements-properties/type-element-xmla.md)元素，`Discover`方法将返回`DISCOVER_LITERALS`行集。  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_LITERALS`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`LiteralName`|`DBTYPE_WSTR`||在行中说明的文字的名称。<br /><br /> 例如： `DBLITERAL_LIKE_PERCENT`|  
|`LiteralValue`|`DBTYPE_WSTR`||实际文字值。<br /><br /> 例如，如果 `LiteralName` 为 `DBLITERAL_LIKE_PERCENT` 并且百分比字符 (`%`) 与 LIKE 子句中的零个或多个字符匹配，则 `LiteralValue` 列的值为“`%`”。|  
|`LiteralInvalidChars`|`DBTYPE_WSTR`||文字中的无效字符。<br /><br /> 例如，如果表名可以包含除数字字符之外的任何字符，则该字符串为“`0123456789`”。|  
|`LiteralInvalidStartingChars`|`DBTYPE_WSTR`||当用作文字的第一个字符时无效的字符。 如果文字能够以任何有效字符开头，则这是 `null`。|  
|`LiteralMaxLength`|`DBTYPE_I4`||文字中的最大字符数。 如果没有最大值或最大值未知，则该值为 –1。|  
|`LiteralNameEnumValue`|`DBTYPE_I4`|||  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 可以使用以下表中的列对 `DISCOVER_LITERALS` 行集进行限制。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`LiteralName`|`DBTYPE_WSTR`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_KEYWORDS 行集&#40;XMLA&#41;](discover-keywords-rowset-xmla.md)  
  
  
