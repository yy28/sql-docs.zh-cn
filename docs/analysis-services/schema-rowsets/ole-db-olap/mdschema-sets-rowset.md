---
title: "MDSCHEMA_SETS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_SETS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_SETS rowset
ms.assetid: abb00dc0-2b83-48d6-b2ba-6615c1488d06
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4820c18992da2aab0ac8e0550a5cadd75ca193bc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemasets-rowset"></a>MDSCHEMA_SETS 行集
  描述当前在数据库中定义的任何集，包括会话作用域的集。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_SETS**行集包含以下各列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|数据库的名称。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|不提供支持。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|多维数据集的名称。|  
|**SET_NAME**|**DBTYPE_WSTR**|将集，作为中指定的名称**CREATE SET**语句。|  
|**作用域**|**DBTYPE_I4**|集的作用域：<br /><br /> **MDSET_SCOPE_GLOBAL** (**1**)<br /><br /> **MDSET_SCOPE_SESSION** (**2**)|  
|**DESCRIPTION**|**DBTYPE_WSTR**|不提供支持。|  
|**表达式**|**DBTYPE_WSTR**|集的表达式。|  
|**维度**|**DBTYPE_WSTR**|集中包含的层次结构的逗号分隔列表。|  
|**SET_CAPTION**|**DBTYPE_WSTR**|与集关联的标签或标题。 标签或标题主要用于显示。|  
|**SET_DISPLAY_FOLDER**|**DBTYPE_WSTR**|标识客户端应用程序用来显示集的显示文件夹路径的字符串。 文件夹级别的分隔符由客户端应用程序定义。 有关工具和客户端提供[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，反斜杠 (\\) 是级别的分隔符。 若要提供多个显示文件夹，请使用分号 （;） 到不同的文件夹。|  
|**SET_EVALUATION_CONTEXT**|**DBTYPE_I4**|集的上下文。 集可以是静态的或动态的。 此列可以为下列值之一：<br /><br /> MDSET_RESOLUTION_STATIC=1<br /><br /> MDSET_RESOLUTION_DYNAMIC=2|  
  
 行集按排序**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_SETS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|可选。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|可选。|  
|**SET_NAME**|**DBTYPE_WSTR**|可选。|  
|**作用域**|**DBTYPE_I4**|可选。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|可选。<br /><br /> 注意： 只有一个层次结构可以包括在内，并仅那些命名集返回其层次结构与限制完全匹配。|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

