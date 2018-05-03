---
title: DISCOVER_XML_METADATA 行集 |Microsoft 文档
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
- DISCOVER_XML_METADATA
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_XML_METADATA rowset
ms.assetid: 0befd026-db1b-43ac-b0e6-734abb56a4b1
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c3c20290bc36ef7fd91d720ed8605e873111e86b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="discoverxmlmetadata-rowset"></a>DISCOVER_XML_METADATA 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  返回描述请求的对象的 XML 文档。 返回的行集始终包含一行和一列。  
  
 如果调用[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法替换**DISCOVER_XML_METATDATA**中的枚举值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)元素，**发现**方法返回**DISCOVER_XML_METATDATA**行集。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_XML_METADATA**行集包含下面的列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**元数据**|**DBTYPE_WSTR**||描述限制所请求对象的 XML 文档。|  
  
 未对此架构行集进行排序。  
  
> [!IMPORTANT]  
>  **DISCOVER_XML_METADATA**行集无法查询使用 SELECT 命令的语法。 但是， **DISCOVER_XML_METADATA**可以使用查询行集<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_XML_METADATA**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**DatabaseID**|**DBTYPE_WSTR**|選擇性。|  
|**DimensionID**|**DBTYPE_WSTR**|選擇性。|  
|**CubeID**|**DBTYPE_WSTR**|選擇性。|  
|**MeasureGroupID**|**DBTYPE_WSTR**|選擇性。|  
|**PartitionID**|**DBTYPE_WSTR**|選擇性。|  
|**PerspectiveID**|**DBTYPE_WSTR**|選擇性。|  
|**DimensionPermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**RoleID**|**DBTYPE_WSTR**|選擇性。|  
|**DatabasePermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**MiningModelID**|**DBTYPE_WSTR**|選擇性。|  
|**MiningModelPermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**DataSourceID**|**DBTYPE_WSTR**|選擇性。|  
|**MiningStructureID**|**DBTYPE_WSTR**|選擇性。|  
|**AggregationDesignID**|**DBTYPE_WSTR**|選擇性。|  
|**TraceID**|**DBTYPE_WSTR**|選擇性。|  
|**MiningStructurePermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**CubePermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**AssemblyID**|**DBTYPE_WSTR**|選擇性。|  
|**MdxScriptID**|**DBTYPE_WSTR**|選擇性。|  
|**DataSourceViewID**|**DBTYPE_WSTR**|選擇性。|  
|**DataSourcePermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**ObjectExpansion**|**DBTYPE_WSTR**|選擇性。|  
  
 此限制， **ObjectExpansion**，可用于的每个主要对象[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 客户端通常使用限制来描述 OLAP 对象的 DDL 才能返回，并使用**ObjectExpansion**限制返回的 DDL 中定义的扩展的程度。 下表指示是否允许枚举值[Alter 元素&#40;XMLA&#41; ](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)命令。  
  
|枚举值|Description|  
|-----------------------|-----------------|  
|**ReferenceOnly**|只返回对所请求对象及其所有递归后代主要对象请求的名称/ID/时间戳/状态。|  
|**ObjectProperties**|展开请求的对象，且不引用包含的对象（包括展开的次要所包含对象）。|  
|**ExpandObject**|与相同*ObjectProperties*，但也会返回名称、 ID 以及包含主要对象的时间戳。|  
|**ExpandFull**|以递归方式将请求的对象完全展开，直至每个所包含对象的最底层。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
