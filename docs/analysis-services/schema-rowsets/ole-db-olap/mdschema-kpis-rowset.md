---
title: MDSCHEMA_KPIS 行集 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
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
- MDSCHEMA_KPIS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_KPIS rowset
ms.assetid: 40fb5112-6a90-4455-82b3-8b6322490222
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3a787f90243bed3fa62cb16281df182a97bfd3ef
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdschemakpis-rowset"></a>MDSCHEMA_KPIS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]描述在数据库中的关键绩效指标 (Kpi)。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_KPIS**行集包含以下各列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|源数据库。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|不提供支持。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|KPI 的父多维数据集。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|KPI 的关联度量值组。<br /><br /> 您可以使用此列确定 KPI 的维数。 如果"**\<NULL >**"，将通过所有度量值组维度 KPI。<br /><br /> 默认值是"**\<NULL >**"。|  
|**KPI_NAME**|**DBTYPE_WSTR**|KPI 的名称。|  
|**KPI_CAPTION**|**DBTYPE_WSTR**|与 KPI 关联的标签或标题。 主要用于显示目的。 如果标题不存在， **KPI_NAME**返回。|  
|**KPI_DESCRIPTION**|**DBTYPE_WSTR**|用户可读的 KPI 说明。|  
|**KPI_DISPLAY_FOLDER**|**DBTYPE_WSTR**|标识客户端应用程序用来显示成员的显示文件夹路径的字符串。 文件夹级别的分隔符由客户端应用程序定义。 有关工具和客户端提供[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，反斜杠 (\\) 是级别的分隔符。 若要提供多个显示文件夹，请使用分号 （;） 到不同的文件夹。|  
|**KPI_VALUE**|**DBTYPE_WSTR**|KPI 值的度量值维度中的成员的唯一名称。|  
|**KPI_GOAL**|**DBTYPE_WSTR**|KPI 目标的度量值维度中的成员的唯一名称。<br /><br /> 返回**NULL**如果没有定义任何目标。|  
|**KPI_STATUS**|**DBTYPE_WSTR**|KPI 状态的度量值维度中的成员的唯一名称。<br /><br /> 返回**NULL**如果没有定义状态。|  
|**KPI_TREND**|**DBTYPE_WSTR**|KPI 趋势的度量值维度中的成员的唯一名称。<br /><br /> 返回**NULL**如果没有定义任何趋势。|  
|**KPI_STATUS_GRAPHIC**|**DBTYPE_WSTR**|KPI 的默认图形表示方式。|  
|**KPI_TREND_GRAPHIC**|**DBTYPE_WSTR**|KPI 的默认图形表示方式。|  
|**KPI_WEIGHT**|**DBTYPE_WSTR**|KPI 权重的度量值维度中的成员的唯一名称。|  
|**KPI_CURRENT_TIME_MEMBER**|**DBTYPE_WSTR**|定义 KPI 临时上下文的时间维度中的成员的唯一名称。<br /><br /> 返回**NULL**如果不存在时间成员定义。|  
|**KPI_PARENT_KPI_NAME**|**DBTYPE_WSTR**|父级 KPI 的名称。|  
|**作用域**|**DBTYPE_I4**|KPI 的作用域。 此 KPI 可以是会话 KPI，也可以是全局 KPI。<br /><br /> 此列可以为下列值之一：<br /><br /> MDKPI_SCOPE_GLOBAL=1<br /><br /> MDKPI_SCOPE_SESSION=2|  
|**批注**|**DBTYPE_WSTR**|（可选）一组格式为 XML 的注释。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_KPIS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|可选。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|可选。|  
|**KPI_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（可选）默认限制是值为**1**。 位图，并使用以下有效的值之一：<br /><br /> **1**多维数据集<br /><br /> **2**维度|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
