---
title: XML 数据类型 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- XML data types [XMLA]
- data types [XML for Analysis]
- XMLA, data types
- XML for Analysis, data types
ms.assetid: 979b5384-90d9-4e09-9286-1d1eafdc4864
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d7a21691474e890ba8614715b18e972d1353b2c6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028857"
---
# <a name="xml-data-types-xmla"></a>XML 数据类型 (XMLA)
  除了 XML 1.0 建议中定义的标准基元类型和派生类型之外，XML for Analysis (XMLA) 1.1 规范还定义了其他数据类型以支持多维数据和表格格式数据的表示形式。  
  
 XMLA 使用下表中列出的数据类型。  
  
|数据类型|Description|  
|----------------|-----------------|  
|Boolean|标准 XML `boolean` 数据类型。|  
|Decimal|标准 XML `decimal` 数据类型。|  
|[EmptyResult](emptyresult-data-type-xmla.md)|`root` 元素上的命名空间。 此命名空间将返回在 XMLA 命令不返回任何结果，因为 XMLA 命令通常不返回结果，或者在出错时[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]执行 XMLA 命令时的实例。|  
|[EnumString](enumstring-data-type-xmla.md)|给定枚举器的命名字符串常量集。|  
|Integer|标准 XML `int` 数据类型。|  
|[MDDataSet](mddataset-data-type-xmla.md)|返回的多维数据*结果*参数[执行](../xml-elements-methods-execute.md)方法。|  
|[结果集](resultset-data-type-xmla.md)|`Execute` 方法返回的自描述 XML 结果集。|  
|[Rowset](rowset-data-type-xmla.md)|嵌入的 XML 架构，结构化的数据源的行返回[发现](../xml-elements-methods-discover.md)方法。|  
|String|XML `string` 数据类型。|  
|UnsignedInt|XML `unsignedInt` 架构类型。|  
  
 有关标准 XML 数据类型的完整说明，请参阅万维网联合会 (WC3) 候选建议。  
  
## <a name="see-also"></a>请参阅  
 [XML 元素&#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)   
 [XML for Analysis &#40;XMLA&#41;引用](../xml-for-analysis-xmla-reference.md)  
  
  