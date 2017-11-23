---
title: "OLE DB for OLAP 架构行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- schema rowsets [Analysis Services], OLE DB for OLAP
- OLE DB for OLAP schema rowsets
- schema rowsets [OLE DB for OLAP]
- rowsets [Analysis Services], OLE DB for OLAP
ms.assetid: 5fad3ecc-407c-4148-862e-ea6119cc7480
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f06af3341034ccc9ddebe1ac6a130be705bdd0cd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="ole-db-for-olap-schema-rowsets"></a>OLE DB for OLAP 架构行集
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口支持下列 OLE DB for OLAP 架构行集。  
  
> [!NOTE]  
>  若要检查特定数据源提供程序是否支持行集，请使用**DISCOVER_ENUMERATIONS**行集[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法。  
  
 你还可以有关这些行集的详细的信息通过搜索主题"OLAP 架构行集"，此时 MSDN 库中[Microsoft Web 站点](http://go.microsoft.com/fwlink/?LinkId=15426)。  
  
## <a name="in-this-section"></a>本节内容  
  
|架构行集<sup>1</sup>|Description|  
|-------------------------------|-----------------|  
|[DISCOVER_INSTANCES 行集](../../../analysis-services/schema-rowsets/ole-db-olap/discover-instances-rowset.md)|介绍服务器上的实例。|  
|[DISCOVER_KEYWORDS 行集 &#40; OLE DB for OLAP &#41;](../../../analysis-services/schema-rowsets/ole-db-olap/discover-keywords-rowset-ole-db-for-olap.md)|枚举该访问接口保留的单词列表。|  
|[MDSCHEMA_ACTIONS 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-actions-rowset.md)|介绍可用于客户端应用程序的操作。|  
|[MDSCHEMA_CUBES 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-cubes-rowset.md)|介绍数据库中的多维数据集的结构。|  
|[MDSCHEMA_DIMENSIONS 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-dimensions-rowset.md)|介绍数据库中的共享维度和专用维度。|  
|[MDSCHEMA_FUNCTIONS 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-functions-rowset.md)|介绍可供连接到数据库的客户端应用程序的函数。|  
|[MDSCHEMA_HIERARCHIES 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)|介绍特定维度中包含的每个层次结构。|  
|[MDSCHEMA_INPUT_DATASOURCES 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)|介绍数据库中定义的数据源。|  
|[MDSCHEMA_KPIS 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-kpis-rowset.md)|介绍数据库中的关键绩效指标 (KPI)。|  
|[MDSCHEMA_LEVELS 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-levels-rowset.md)|介绍特定层次结构中的每个级别。|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md)|枚举度量值组的维度。|  
|[MDSCHEMA_MEASUREGROUPS 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset.md)|介绍数据库中的度量值组。|  
|[MDSCHEMA_MEASURES 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measures-rowset.md)|介绍多维数据集中的每个度量值。|  
|[MDSCHEMA_MEMBERS 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-members-rowset.md)|介绍数据库中的成员。|  
|[MDSCHEMA_PROPERTIES 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)|介绍数据库中的成员的属性。|  
|[MDSCHEMA_SETS 行集](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-sets-rowset.md)|描述当前在数据库中定义的任何集，包括会话作用域的集。|  
  
 <sup>1</sup>此处列出的所有架构行集都支持的 MSOLAP 数据源提供程序为[!INCLUDE[msCoName](../../../includes/msconame-md.md)]XMLA 提供程序。  
  
## <a name="see-also"></a>另请参阅  
 [DISCOVER_ENUMERATORS 行集](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)   
 [Analysis Services 架构行集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
