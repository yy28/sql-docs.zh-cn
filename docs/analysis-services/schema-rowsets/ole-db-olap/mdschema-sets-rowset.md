---
title: MDSCHEMA_SETS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e3750594327d247cbb9f8abbc577c29027d1c92f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemasets-rowset"></a>MDSCHEMA_SETS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SET_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**作用域**|**DBTYPE_I4**|選擇性。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|選擇性。<br /><br /> 注意： 只有一个层次结构可以包括在内，并仅那些命名集返回其层次结构与限制完全匹配。|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
