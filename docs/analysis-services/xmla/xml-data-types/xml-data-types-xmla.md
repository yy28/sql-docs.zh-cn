---
title: XML 数据类型 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c52717a6f061f4708b2d3e46c6d34f837b2039af
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34573779"
---
# <a name="xml-data-types-xmla"></a>XML 数据类型 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  除了 XML 1.0 建议中定义的标准基元类型和派生类型之外，XML for Analysis (XMLA) 1.1 规范还定义了其他数据类型以支持多维数据和表格格式数据的表示形式。  
  
 XMLA 使用下表中列出的数据类型。  
  
|数据类型|Description|  
|----------------|-----------------|  
|Boolean|标准的 XML**布尔**数据类型。|  
|Decimal|标准的 XML**十进制**数据类型。|  
|[EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|上的命名空间**根**元素。 当 XMLA 命令不返回任何结果，因为 XMLA 命令通常不返回结果，或者因为出错 Analysis Services 实例上执行 XMLA 命令时，将返回此命名空间。|  
|[EnumString](../../../analysis-services/xmla/xml-data-types/enumstring-data-type-xmla.md)|给定枚举器的命名字符串常量集。|  
|Integer|标准的 XML **int**数据类型。|  
|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)|返回的多维数据*结果*参数[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。|  
|[结果集](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|自我描述 XML 结果集返回**执行**方法。|  
|[Rowset](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)|嵌入的 XML 架构，结构化的数据源的行返回[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法。|  
|String|XML**字符串**数据类型。|  
|UnsignedInt|XML **unsignedInt**架构类型。|  
  
 有关标准 XML 数据类型的完整说明，请参阅万维网联合会 (WC3) 候选建议。  
  
## <a name="see-also"></a>另请参阅
 [XML 元素&#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML for Analysis &#40;XMLA&#41;引用](../../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
