---
title: MDSCHEMA_SETS 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_SETS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_SETS rowset
ms.assetid: abb00dc0-2b83-48d6-b2ba-6615c1488d06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1e3008fc6b56146c22a7508398dcc3896a697644
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059520"
---
# <a name="mdschemasets-rowset"></a>MDSCHEMA_SETS 行集
  描述当前在数据库中定义的任何集，包括会话作用域的集。  
  
## <a name="rowset-columns"></a>行集列  
 `MDSCHEMA_SETS`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||数据库的名称。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不提供支持。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||多维数据集的名称。|  
|`SET_NAME`|`DBTYPE_WSTR`||在 `CREATE SET` 语句中指定的集的名称。|  
|`SCOPE`|`DBTYPE_I4`||集的作用域：<br /><br /> -   `MDSET_SCOPE_GLOBAL` (`1`)<br />-   `MDSET_SCOPE_SESSION` (`2`)|  
|`DESCRIPTION`|`DBTYPE_WSTR`||不提供支持。|  
|`EXPRESSION`|`DBTYPE_WSTR`||集的表达式。|  
|`DIMENSIONS`|`DBTYPE_WSTR`||集中包含的层次结构的逗号分隔列表。|  
|`SET_CAPTION`|`DBTYPE_WSTR`||与集关联的标签或标题。 标签或标题主要用于显示。|  
|`SET_DISPLAY_FOLDER`|`DBTYPE_WSTR`||标识客户端应用程序用来显示集的显示文件夹路径的字符串。 文件夹级别的分隔符由客户端应用程序定义。 有关工具和客户端提供的[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，反斜杠 (\\) 作为级别分隔符。 若要提供多个显示文件夹，请使用分号 （;） 来分隔文件夹。|  
|`SET_EVALUATION_CONTEXT`|`DBTYPE_I4`||集的上下文。 集可以是静态的或动态的。<br /><br /> 此列可以为下列值之一：<br /><br /> -MDSET_RESOLUTION_STATIC = 1<br />-MDSET_RESOLUTION_DYNAMIC = 2|  
  
 行集按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制列  
 `MDSCHEMA_SETS`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|可选。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|可选。|  
|`SET_NAME`|`DBTYPE_WSTR`|可选。|  
|`SCOPE`|`DBTYPE_I4`|可选。|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|可选。 **注意：** 只有一个层次结构可以包含，并且仅的命名集将返回其层次结构与限制完全匹配。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  
