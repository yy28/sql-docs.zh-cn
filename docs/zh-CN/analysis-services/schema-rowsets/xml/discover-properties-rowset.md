---
title: DISCOVER_PROPERTIES 行集 |Microsoft 文档
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
- DISCOVER_PROPERTIES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_PROPERTIES rowset
ms.assetid: 3e2b50e2-3855-4091-8b02-4968e8e57d4c
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f37cf116c4d31dbd63ba13b575a91fa042350863
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="discoverproperties-rowset"></a>DISCOVER_PROPERTIES 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  返回指定数据源的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口支持的标准属性和特定于访问接口的属性的信息和值列表。 不支持的属性不在返回结果集中列出。  
  
 如果调用[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法替换**DISCOVER_PROPERTIES**中的枚举值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)元素，**发现**方法返回**DISCOVER_PROPERTIES**行集...  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_PROPERTIES**行集包含以下各列。  
  
|列名|类型|长度|Description|  
|-----------------|----------|------------|-----------------|  
|**属性名**|**DBTYPE_WSTR**||属性的名称。|  
|**PropertyDescription**|**DBTYPE_WSTR**||属性的可本地化文本说明。 可能会返回**NULL**。|  
|**PropertyType**|**DBTYPE_WSTR**||属性的 XML 数据类型。<br /><br /> 可能会返回**NULL**。|  
|**PropertyAccessType**|**DBTYPE_WSTR**||属性的访问权限。 该值可以为**读取**，**编写**，或**ReadWrite**。|  
|**IsRequired**|**DBTYPE_BOOL**||指示是否需要属性的布尔值。<br /><br /> 如果需要属性，则为 True；如果不需要属性，则为 False。<br /><br /> 可能会返回**NULL**。|  
|**Value**|**DBTYPE_WSTR**||属性的当前值。<br /><br /> 可能会返回**NULL**。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_PROPERTIES**行集可限制下表中列出的列上。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**属性名**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
