---
title: "XML 数据类型 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- XML data types [XMLA]
- data types [XML for Analysis]
- XMLA, data types
- XML for Analysis, data types
ms.assetid: 979b5384-90d9-4e09-9286-1d1eafdc4864
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ba74f6ec5cb8ad35d4cdbb76e408bcb6cc203dea
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="xml-data-types-xmla"></a>XML 数据类型 (XMLA)
  除了 XML 1.0 建议中定义的标准基元类型和派生类型之外，XML for Analysis (XMLA) 1.1 规范还定义了其他数据类型以支持多维数据和表格格式数据的表示形式。  
  
 XMLA 使用下表中列出的数据类型。  
  
|数据类型|Description|  
|----------------|-----------------|  
|Boolean|标准的 XML**布尔**数据类型。|  
|Decimal|标准的 XML**十进制**数据类型。|  
|[EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|上的命名空间**根**元素。 此命名空间将返回在 XMLA 命令不返回任何结果，因为 XMLA 命令通常不返回结果，或者在出错时[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]执行 XMLA 命令时的实例。|  
|[EnumString](../../../analysis-services/xmla/xml-data-types/enumstring-data-type-xmla.md)|给定枚举器的命名字符串常量集。|  
|Integer|标准的 XML **int**数据类型。|  
|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)|返回的多维数据*结果*参数[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。|  
|[结果集](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|自我描述 XML 结果集返回**执行**方法。|  
|[行集](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)|嵌入的 XML 架构，结构化的数据源的行返回[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法。|  
|字符串|XML**字符串**数据类型。|  
|UnsignedInt|XML **unsignedInt**架构类型。|  
  
 有关标准 XML 数据类型的完整说明，请参阅万维网联合会 (WC3) 候选建议。  
  
## <a name="see-also"></a>另请参阅  
 [XML 元素 &#40;XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML for Analysis &#40;XMLA &#41;引用](../../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
