---
title: DISCOVER_PROPERTIES 行集 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DISCOVER_PROPERTIES
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_PROPERTIES rowset
ms.assetid: 3e2b50e2-3855-4091-8b02-4968e8e57d4c
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: af566467345e29362a7b2fdd2c5bda04a35a6dd5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123722"
---
# <a name="discoverproperties-rowset"></a>DISCOVER_PROPERTIES 行集
  返回指定数据源的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口支持的标准属性和特定于访问接口的属性的信息和值列表。 不支持的属性不在返回结果集中列出。  
  
 如果调用[发现](../../xmla/xml-elements-methods-discover.md)方法替换`DISCOVER_PROPERTIES`中的枚举值[RequestType](../../xmla/xml-elements-properties/type-element-xmla.md)元素，`Discover`方法返回`DISCOVER_PROPERTIES`行集...  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_PROPERTIES`行集包含以下各列。  
  
|列名|类型|长度|Description|  
|-----------------|----------|------------|-----------------|  
|`PropertyName`|`DBTYPE_WSTR`||属性的名称。|  
|`PropertyDescription`|`DBTYPE_WSTR`||属性的可本地化文本说明。 可能会返回 `NULL`。|  
|`PropertyType`|`DBTYPE_WSTR`||属性的 XML 数据类型。<br /><br /> 可能会返回 `NULL`。|  
|`PropertyAccessType`|`DBTYPE_WSTR`||属性的访问权限。 该值可以是 `Read`、`Write` 或 `ReadWrite`。|  
|`IsRequired`|`DBTYPE_BOOL`||指示是否需要属性的布尔值。<br /><br /> 如果需要属性，则为 True；如果不需要属性，则为 False。<br /><br /> 可能会返回 `NULL`。|  
|`Value`|`DBTYPE_WSTR`||属性的当前值。<br /><br /> 可能会返回 `NULL`。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 对于 `DISCOVER_PROPERTIES` 行集，可对下表中列出的列进行限制。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`PropertyName`|`DBTYPE_WSTR`||  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  