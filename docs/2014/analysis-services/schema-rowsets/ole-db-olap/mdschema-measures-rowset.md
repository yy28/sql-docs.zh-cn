---
title: MDSCHEMA_MEASURES 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_MEASURES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASURES rowset
ms.assetid: 6ff5bd1a-aad0-49b8-9f8d-7df2637caacf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f421e3ebd93af0eb5fe175c0d94d28ab8509289
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094267"
---
# <a name="mdschemameasures-rowset"></a>MDSCHEMA_MEASURES 行集
  描述多维数据集中的每个度量值。  
  
## <a name="rowset-columns"></a>行集列  
 `MDSCHEMA_MEASURES`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||此度量值所属的目录的名称。 如果提供程序不支持目录，则为 `NULL`。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||此度量值所属的架构的名称。 `NULL` 如果提供程序不支持架构。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||此度量值所属的多维数据集的名称。|  
|`MEASURE_NAME`|`DBTYPE_WSTR`||度量值的名称。|  
|`MEASURE_UNIQUE_NAME`|`DBTYPE_WSTR`||度量值的唯一名称。 对于通过限定生成唯一名称的访问接口，此名称的各组成部分之间用分隔符分隔。|  
|`MEASURE_CAPTION`|`DBTYPE_WSTR`||与度量值关联的标签或标题。 主要用于显示目的。 如果不存在标题，`MEASURE_NAME`返回。|  
|`MEASURE_GUID`|`DBTYPE_GUID`||不提供支持。|  
|`MEASURE_AGGREGATOR`|`DBTYPE_I4`||用于标识度量值派生方式的枚举。 可以是下列值之一：<br /><br /> -   `MDMEASURE_AGGR_SUM` (`1`) 标识度量值聚合来自`SUM`。<br />-   `MDMEASURE_AGGR_COUNT` (`2`) 标识度量值聚合来自`COUNT`。<br />-   **MDMEASURE_AGGR_MIN** (`3`) 标识度量值聚合来自`MIN`。<br />-   **MDMEASURE_AGGR_MAX** (`4`) 标识度量值聚合来自`MAX`。<br />-   `MDMEASURE_AGGR_AVG` (`5`) 标识度量值聚合来自`AVG`。<br />-   `MDMEASURE_AGGR_VAR` (`6`) 标识度量值聚合来自`VAR`。<br />-   `MDMEASURE_AGGR_STD` (`7`) 标识度量值聚合来自`STDEV`。<br />-   `MDMEASURE_AGGR_DST` (`8`) 标识度量值聚合来自`DISTINCT COUNT`。<br />-   `MDMEASURE_AGGR_NONE` (`9`) 标识度量值聚合来自`NONE`。<br />-   `MDMEASURE_AGGR_AVGCHILDREN` (`10`) 标识度量值聚合来自`AVERAGEOFCHILDREN`。<br />-   `MDMEASURE_AGGR_FIRSTCHILD` (`11`) 标识度量值聚合来自`FIRSTCHILD`。<br />-   `MDMEASURE_AGGR_LASTCHILD` (`12`) 标识度量值聚合来自`LASTCHILD`。<br />-   `MDMEASURE_AGGR_FIRSTNONEMPTY` (`13`) 标识度量值聚合来自`FIRSTNONEMPTY`，<br />-   `MDMEASURE_AGGR_LASTNONEMPTY` (`14`) 标识度量值聚合来自`LASTNONEMPTY`。<br />-   `MDMEASURE_AGGR_BYACCOUNT` (`15`) 标识度量值聚合来自`BYACCOUNT`。<br />-   `MDMEASURE_AGGR_CALCULATED` (`127`) 标识度量值不是上述所有函数的公式从派生。<br />-   `MDMEASURE_AGGR_UNKNOWN` (`0`) 标识度量值从未知的聚合函数或公式派生。|  
|`DATA_TYPE`|`DBTYPE_UI2`||度量值的数据类型。|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||如果度量值对象的数据类型为精确数字，则为属性的最大精度。 对于所有其他属性类型，则为 `NULL`。|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||如果度量值对象的类型指示符为 `DBTYPE_NUMERIC` 或 `DBTYPE_DECIMAL`，则为小数点右侧的位数。 否则，此值是`NULL`。|  
|`MEASURE_UNITS`|`DBTYPE_WSTR`||不支持|  
|`DESCRIPTION`|`DBTYPE_WSTR`||度量值的可读说明。 如果不存在说明，则为 `NULL`。|  
|`EXPRESSION`|`DBTYPE_WSTR`||成员的表达式。|  
|`MEASURE_IS_VISIBLE`|`DBTYPE_BOOL`||始终返回 True 的布尔值。 如果相应度量值不可见，则架构行集中也不会包含该度量值。|  
|`LEVELS_LIST`|`DBTYPE_WSTR`||始终返回 `NULL` 的字符串。|  
|`MEASURE_NAME_SQL_COLUMN_NAME`|`DBTYPE_WSTR`||SQL 查询中与相应度量值的名称相对应的列名称。|  
|`MEASURE_UNQUALIFIED_CAPTION`|`DBTYPE_WSTR`||未用度量值组名称限定的度量值名称。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||度量值所属的度量值组的名称。|  
|`MEASURE_DISPLAY_FOLDER`|`DBTYPE_WSTR`||在用户界面中显示度量值时所使用的路径。 文件夹名称将使用分号分隔。 嵌套的文件夹由反斜杠 (\\)。|  
|`DEFAULT_FORMAT_STRING`|`DBTYPE_WSTR`||度量值的默认格式字符串。|  
  
 行集按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME`、`MEASURE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制列  
 `MDSCHEMA_MEASURES`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|可选。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|可选。|  
|`MEASURE_NAME`|`DBTYPE_WSTR`|可选。|  
|`MEASURE_UNIQUE_NAME`|`DBTYPE_WSTR`|可选。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|（可选）使用以下有效值之一位图：<br /><br /> -1 的多维数据集<br />-2 个维度<br /><br /> 默认限制的值为 1。|  
|`MEASURE_VISIBILITY`|`DBTYPE_UI2`|（可选）使用以下有效值之一位图：<br /><br /> -1 的可见性<br />-2 不可见<br /><br /> 默认限制的值为 1。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  
