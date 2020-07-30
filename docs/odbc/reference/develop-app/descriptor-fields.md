---
title: 描述符字段 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d363c3e42a97c5d520c1a693ebed935b202b7247
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362557"
---
# <a name="descriptor-fields"></a>描述符字段
描述符包含完全描述列或参数的*标头*和*记录*字段。  
  
 描述符包含以下标头字段的单个副本。 更改标题字段将影响所有列或参数。  

:::row:::
    :::column:::
        SQL_DESC_ALLOC_TYPE  
        SQL_DESC_ARRAY_SIZE  
        SQL_DESC_ARRAY_STATUS_PTR  
        SQL_DESC_BIND_OFFSET_PTR  
    :::column-end:::
    :::column:::
        SQL_DESC_BIND_TYPE  
        SQL_DESC_COUNT  
        SQL_DESC_ROWS_PROCESSED_PTR  
    :::column-end:::
:::row-end:::

 描述符包含零个或多个描述符记录。 每条记录都描述列或参数，具体取决于描述符的类型。 绑定新的列或参数时，会将新的记录添加到描述符中。 如果列或参数未绑定，则会从描述符中删除一条记录。 每个记录都包含以下字段的单个副本：  

:::row:::
    :::column:::
        SQL_DESC_AUTO_UNIQUE_VALUE  
        SQL_DESC_BASE_COLUMN_NAME  
        SQL_DESC_BASE_TABLE_NAME  
        SQL_DESC_CASE_SENSITIVE  
        SQL_DESC_CATALOG_NAME  
        SQL_DESC_CONCISE_TYPE  
        SQL_DESC_DATA_PTR  
        SQL_DESC_DATETIME_INTERVAL_CODE  
        SQL_DESC_DATETIME_INTERVAL_PRECISION  
        SQL_DESC_DISPLAY_SIZE  
        SQL_DESC_FIXED_PREC_SCALE  
        SQL_DESC_INDICATOR_PTR  
        SQL_DESC_LABEL  
        SQL_DESC_LENGTH  
        SQL_DESC_LITERAL_PREFIX  
        SQL_DESC_LITERAL_SUFFIX  
    :::column-end:::
    :::column:::
        SQL_DESC_LOCAL_TYPE_NAME  
        SQL_DESC_NAME  
        SQL_DESC_NULLABLE  
        SQL_DESC_OCTET_LENGTH  
        SQL_DESC_OCTET_LENGTH_PTR  
        SQL_DESC_PARAMETER_TYPE  
        SQL_DESC_PRECISION  
        SQL_DESC_SCALE  
        SQL_DESC_SCHEMA_NAME  
        SQL_DESC_SEARCHABLE  
        SQL_DESC_TABLE_NAME  
        SQL_DESC_TYPE  
        SQL_DESC_TYPE_NAME  
        SQL_DESC_UNNAMED  
        SQL_DESC_UNSIGNED  
        SQL_DESC_UPDATABLE  
    :::column-end:::
:::row-end:::

 许多语句特性对应于描述符的标头字段。 通过调用**SQLSetStmtAttr**来设置这些属性，并通过调用**SQLSetDescField**设置相应的描述符标头字段具有相同的效果。 这同样适用于**SQLGetStmtAttr**和**SQLGetDescField**，这两个参数都检索相同的信息。 调用语句函数而不是描述符函数的优点是不需要检索描述符句柄。  
  
 可以通过设置语句特性来设置以下标头字段：  

:::row:::
    :::column:::
        SQL_DESC_ARRAY_SIZE  
        SQL_DESC_ARRAY_STATUS_PTR  
        SQL_DESC_BIND_OFFSET_PTR  
    :::column-end:::
    :::column:::
        SQL_DESC_BIND_TYPE  
        SQL_DESC_ROWS_PROCESSED_PTR  
    :::column-end:::
:::row-end:::

 本部分包含以下主题。  
  
-   [记录计数](../../../odbc/reference/develop-app/record-count.md)  
  
-   [绑定描述符记录](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [延迟的字段](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [一致性检查](../../../odbc/reference/develop-app/consistency-check.md)
