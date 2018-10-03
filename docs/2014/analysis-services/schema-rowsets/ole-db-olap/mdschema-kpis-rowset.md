---
title: MDSCHEMA_KPIS 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_KPIS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_KPIS rowset
ms.assetid: 40fb5112-6a90-4455-82b3-8b6322490222
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 77f6dc3fd3f8e9c92fe1d840c9af646269e0effc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124457"
---
# <a name="mdschemakpis-rowset"></a>MDSCHEMA_KPIS 行集
  介绍数据库中的关键绩效指标 (KPI)。  
  
## <a name="rowset-columns"></a>行集列  
 `MDSCHEMA_KPIS`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||源数据库。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不提供支持。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||KPI 的父多维数据集。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||KPI 的关联度量值组。<br /><br /> 您可以使用此列确定 KPI 的维数。 如果"**\<NULL >**"，由所有度量值组维度所 KPI。<br /><br /> 默认值是"**\<NULL >**"。|  
|`KPI_NAME`|`DBTYPE_WSTR`||KPI 的名称。|  
|`KPI_CAPTION`|`DBTYPE_WSTR`||与 KPI 关联的标签或标题。 主要用于显示目的。 如果不存在标题，`KPI_NAME`返回。|  
|`KPI_DESCRIPTION`|`DBTYPE_WSTR`||用户可读的 KPI 说明。|  
|`KPI_DISPLAY_FOLDER`|`DBTYPE_WSTR`||标识客户端应用程序用来显示成员的显示文件夹路径的字符串。 文件夹级别的分隔符由客户端应用程序定义。 有关工具和客户端提供的[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，反斜杠 (\\) 作为级别分隔符。 若要提供多个显示文件夹，请使用分号 （;） 来分隔文件夹。|  
|`KPI_VALUE`|`DBTYPE_WSTR`||KPI 值的度量值维度中的成员的唯一名称。|  
|`KPI_GOAL`|`DBTYPE_WSTR`||KPI 目标的度量值维度中的成员的唯一名称。<br /><br /> 如果未定义目标，则返回 `NULL`。|  
|`KPI_STATUS`|`DBTYPE_WSTR`||KPI 状态的度量值维度中的成员的唯一名称。<br /><br /> 如果未定义状态，则返回 `NULL`。|  
|`KPI_TREND`|`DBTYPE_WSTR`||KPI 趋势的度量值维度中的成员的唯一名称。<br /><br /> 如果未定义趋势，则返回 `NULL`。|  
|`KPI_STATUS_GRAPHIC`|`DBTYPE_WSTR`||KPI 的默认图形表示方式。|  
|`KPI_TREND_GRAPHIC`|`DBTYPE_WSTR`||KPI 的默认图形表示方式。|  
|`KPI_WEIGHT`|`DBTYPE_WSTR`||KPI 权重的度量值维度中的成员的唯一名称。|  
|`KPI_CURRENT_TIME_MEMBER`|`DBTYPE_WSTR`||定义 KPI 临时上下文的时间维度中的成员的唯一名称。<br /><br /> 如果未定义时间成员，则返回 `NULL`。|  
|`KPI_PARENT_KPI_NAME`|`DBTYPE_WSTR`||父级 KPI 的名称。|  
|`SCOPE`|`DBTYPE_I4`||KPI 的作用域。 此 KPI 可以是会话 KPI，也可以是全局 KPI。<br /><br /> 此列可以为下列值之一：<br /><br /> -MDKPI_SCOPE_GLOBAL = 1<br />-MDKPI_SCOPE_SESSION = 2|  
|`ANNOTATIONS`|`DBTYPE_WSTR`||（可选）一组格式为 XML 的注释。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 `MDSCHEMA_KPIS`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|可选。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|可选。|  
|`KPI_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|（可选）使用以下有效值之一位图：<br /><br /> -   `1` 多维数据集<br />-   `2` 维度<br /><br /> 默认限制的值为 `1`。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  
