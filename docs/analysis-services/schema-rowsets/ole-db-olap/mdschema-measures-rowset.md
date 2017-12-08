---
title: "MDSCHEMA_MEASURES 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
apiname: MDSCHEMA_MEASURES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_MEASURES rowset
ms.assetid: 6ff5bd1a-aad0-49b8-9f8d-7df2637caacf
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b6e2e862d6ad09659a19ce60498e2f5f06810eb2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="mdschemameasures-rowset"></a>MDSCHEMA_MEASURES 行集
  描述多维数据集中的每个度量值。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_MEASURES**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||此度量值所属的目录的名称。 **NULL**如果提供程序不支持目录。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||此度量值所属的架构的名称。 **NULL**如果提供程序不支持架构。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||此度量值所属的多维数据集的名称。|  
|**MEASURE_NAME**|**DBTYPE_WSTR**||度量值的名称。|  
|**MEASURE_UNIQUE_NAME**|**DBTYPE_WSTR**||度量值的唯一名称。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|**MEASURE_CAPTION**|**DBTYPE_WSTR**||与度量值关联的标签或标题。 主要用于显示目的。 如果标题不存在， **MEASURE_NAME**返回。|  
|**MEASURE_GUID**|**DBTYPE_GUID**||不提供支持。|  
|**MEASURE_AGGREGATOR**|**DBTYPE_I4**||用于标识度量值派生方式的枚举。 可以是以下值之一：<br /><br /> **MDMEASURE_AGGR_SUM** (**1**) 标识该度量值聚合来自**总和**。<br /><br /> **MDMEASURE_AGGR_COUNT** (**2**) 标识该度量值聚合来自**计数**。<br /><br /> **MDMEASURE_AGGR_MIN** (**3**) 标识该度量值聚合来自**MIN**。<br /><br /> **MDMEASURE_AGGR_MAX** (**4**) 标识该度量值聚合来自**最大**。<br /><br /> **MDMEASURE_AGGR_AVG** (**5**) 标识该度量值聚合来自**AVG**。<br /><br /> **MDMEASURE_AGGR_VAR** (**6**) 标识该度量值聚合来自**VAR**。<br /><br /> **MDMEASURE_AGGR_STD** (**7**) 标识该度量值聚合来自**STDEV**。<br /><br /> **MDMEASURE_AGGR_DST** (**8**) 标识该度量值聚合来自**非重复计数**。<br /><br /> **MDMEASURE_AGGR_NONE** (**9**) 标识该度量值聚合来自**NONE**。<br /><br /> **MDMEASURE_AGGR_AVGCHILDREN** (**10**) 标识该度量值聚合来自**AVERAGEOFCHILDREN**。<br /><br /> **MDMEASURE_AGGR_FIRSTCHILD** (**11**) 标识该度量值聚合来自**FIRSTCHILD**。<br /><br /> **MDMEASURE_AGGR_LASTCHILD** (**12**) 标识该度量值聚合来自**LASTCHILD**。<br /><br /> **MDMEASURE_AGGR_FIRSTNONEMPTY** (**13**) 标识该度量值聚合来自**FIRSTNONEMPTY**，<br /><br /> **MDMEASURE_AGGR_LASTNONEMPTY** (**14**) 标识该度量值聚合来自**LASTNONEMPTY**。<br /><br /> **MDMEASURE_AGGR_BYACCOUNT** (**15**) 标识该度量值聚合来自**BYACCOUNT**。<br /><br /> **MDMEASURE_AGGR_CALCULATED** (**127**) 标识，该度量值派生自不是上述任何单个函数的公式。<br /><br /> **MDMEASURE_AGGR_UNKNOWN** (**0**) 标识，该度量值派生自一个未知的聚合函数或公式。|  
|**DATA_TYPE**|**DBTYPE_UI2**||度量值的数据类型。|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||如果度量值对象的数据类型为精确数字，则为属性的最大精度。 **NULL**对于所有其他属性类型。|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||如果度量值对象的类型指示符为小数点右侧的数字个数**DBTYPE_NUMERIC**或**DBTYPE_DECIMAL**。 否则，此值是**NULL**。|  
|**MEASURE_UNITS**|**DBTYPE_WSTR**||不支持|  
|**DESCRIPTION**|**DBTYPE_WSTR**||度量值的可读说明。 **NULL**如果没有任何其他说明存在。|  
|**表达式**|**DBTYPE_WSTR**||成员的表达式。|  
|**MEASURE_IS_VISIBLE**|**DBTYPE_BOOL**||始终返回 True 的布尔值。 如果相应度量值不可见，则架构行集中也不会包含该度量值。|  
|**LEVELS_LIST**|**DBTYPE_WSTR**||始终返回一个字符串**NULL**。|  
|**MEASURE_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**||SQL 查询中与相应度量值的名称相对应的列名称。|  
|**MEASURE_UNQUALIFIED_CAPTION**|**DBTYPE_WSTR**||未用度量值组名称限定的度量值名称。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||度量值所属的度量值组的名称。|  
|**MEASURE_DISPLAY_FOLDER**|**DBTYPE_WSTR**||在用户界面中显示度量值时所使用的路径。 文件夹名称将使用分号分隔。 通过反斜杠来指示嵌套的文件夹 (\\)。|  
|**DEFAULT_FORMAT_STRING**|**DBTYPE_WSTR**||度量值的默认格式字符串。|  
  
 行集按排序**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **MEASURE_NAME**。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_MEASURES**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|可选。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|可选。|  
|**MEASURE_NAME**|**DBTYPE_WSTR**|可选。|  
|**MEASURE_UNIQUE_NAME**|**DBTYPE_WSTR**|可选。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**MEASURE_VISIBILITY**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用以下有效的值之一：<br /><br /> 1 可见<br /><br /> 2 不可见|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
