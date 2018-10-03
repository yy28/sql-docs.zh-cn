---
title: XML 数据类型 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dba93ca0c4b066498455efeac7470a65d291941a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191198"
---
# <a name="xml-data-types-xmla"></a>XML 数据类型 (XMLA)
  除了 XML 1.0 建议中定义的标准基元类型和派生类型之外，XML for Analysis (XMLA) 1.1 规范还定义了其他数据类型以支持多维数据和表格格式数据的表示形式。  
  
 XMLA 使用下表中列出的数据类型。  
  
|数据类型|Description|  
|----------------|-----------------|  
|Boolean|标准 XML `boolean` 数据类型。|  
|Decimal|标准 XML `decimal` 数据类型。|  
|[EmptyResult](emptyresult-data-type-xmla.md)|`root` 元素上的命名空间。 XMLA 命令不返回结果，因为 XMLA 命令正常情况下不返回结果，或者因为发生错误时，将返回此命名空间[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例执行 XMLA 命令时。|  
|[EnumString](enumstring-data-type-xmla.md)|给定枚举器的命名字符串常量集。|  
|Integer|标准 XML `int` 数据类型。|  
|[MDDataSet](mddataset-data-type-xmla.md)|返回的多维数据*结果*的参数[Execute](../xml-elements-methods-execute.md)方法。|  
|[结果集](resultset-data-type-xmla.md)|`Execute` 方法返回的自描述 XML 结果集。|  
|[Rowset](rowset-data-type-xmla.md)|返回的行从数据源，由嵌入式 XML 架构，结构化[发现](../xml-elements-methods-discover.md)方法。|  
|String|XML `string` 数据类型。|  
|UnsignedInt|XML `unsignedInt` 架构类型。|  
  
 有关标准 XML 数据类型的完整说明，请参阅万维网联合会 (WC3) 候选建议。  
  
## <a name="see-also"></a>请参阅  
 [XML 元素&#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)   
 [XML for Analysis &#40;XMLA&#41;引用](../xml-for-analysis-xmla-reference.md)  
  
  
