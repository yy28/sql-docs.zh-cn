---
title: 描述符字段 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cfab4928192cce12069044264c6efb990080b75b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="descriptor-fields"></a>描述符字段
描述符包含*标头*和*记录*完整地描述列或参数的字段。  
  
 描述符包含以下标头字段的单个副本。 更改标头字段会影响所有列或参数。  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 描述符包含零个或多个描述符记录。 每个记录描述的一个列或参数，具体取决于描述符的类型。 当绑定的新列或参数时，一条新记录将添加到描述符。 未绑定的列或参数时，将从描述符中删除一条记录。 每个记录包含以下字段的单个副本：  
  
|||  
|-|-|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_DESC_LOCAL_TYPE_NAME|  
|SQL_DESC_BASE_COLUMN_NAME|SQL_DESC_NAME|  
|SQL_DESC_BASE_TABLE_NAME|SQL_DESC_NULLABLE|  
|SQL_DESC_CASE_SENSITIVE|SQL_DESC_OCTET_LENGTH|  
|SQL_DESC_CATALOG_NAME|SQL_DESC_OCTET_LENGTH_PTR|  
|SQL_DESC_CONCISE_TYPE|SQL_DESC_PARAMETER_TYPE|  
|SQL_DESC_DATA_PTR|SQL_DESC_PRECISION|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_DESC_SCALE|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQL_DESC_SCHEMA_NAME|  
|SQL_DESC_DISPLAY_SIZE|SQL_DESC_SEARCHABLE|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_DESC_TABLE_NAME|  
|SQL_DESC_INDICATOR_PTR|SQL_DESC_TYPE|  
|SQL_DESC_LABEL|SQL_DESC_TYPE_NAME|  
|SQL_DESC_LENGTH|SQL_DESC_UNNAMED|  
|SQL_DESC_LITERAL_PREFIX|SQL_DESC_UNSIGNED|  
|SQL_DESC_LITERAL_SUFFIX|SQL_DESC_UPDATABLE|  
  
 许多语句特性对应于描述符的标头字段中。 将通过调用这些特性设置**SQLSetStmtAttr**并通过调用设置相应的描述符标头字段**SQLSetDescField**具有相同的效果。 同样适用于**SQLGetStmtAttr**和**SQLGetDescField**，这两种中检索相同信息。 调用而不是描述符函数语句函数具有的描述符句柄没有要检索的优点。  
  
 通过设置语句特性，可以设置以下标头字段：  
  
|||  
|-|-|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 本部分包含以下主题。  
  
-   [记录计数](../../../odbc/reference/develop-app/record-count.md)  
  
-   [绑定描述符记录](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [延迟的字段](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [一致性检查](../../../odbc/reference/develop-app/consistency-check.md)
