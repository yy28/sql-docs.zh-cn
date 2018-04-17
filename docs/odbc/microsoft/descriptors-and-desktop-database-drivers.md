---
title: 描述符和桌面数据库驱动程序 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3c1cf39e841e57e4ef836f042cea41240f7f7bfe
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="descriptors-and-desktop-database-drivers"></a>描述符和桌面数据库驱动程序
描述符是一种数据结构，其中包含有关列数据或动态参数的信息。 **SQLGetDescField**可以用于检索下面列出的受支持的描述符。 实现参数描述符 (IPD) 不会自动填充因为**SQLDescribeParam**不支持。 不可通过 Jet （如 SQL_DESC_BASE_TABLE_NAME) 的描述符字段也不支持。  
  
 有关 Jet 支持描述符字段的详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。  
  
 有关描述符的详细信息，请参阅"描述符"下的主题中*ODBC 程序员参考*。  
  
|描述符字段|支持级别|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Supported|  
|SQL_DESC_ARRAY_SIZE|仅对 ARD 的支持|  
|SQL_DESC_ARRAY_STATUS_PTR|Supported|  
|SQL_DESC_BIND_OFFSET_PTR|Supported|  
|SQL_DESC_BIND_TYPE|Supported|  
|SQL_DESC_COUNT|Supported|  
|SQL_DESC_ROWS_PROCESSED_PTR|仅对 ARD 的支持|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Supported|  
|SQL_DESC_BASE_COLUMN_NAME|支持 （新增）|  
|SQL_DESC_BASE_TABLE_NAME|支持 （新增）|  
|SQL_DESC_CASE_SENSITIVE|始终为 FALSE|  
|SQL_DESC_CATALOG_NAME|不支持|  
|SQL_DESC_CONCISE_TYPE|Supported|  
|SQL_DESC_DATA_PTR|Supported|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Supported|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|间隔 C 类型支持|  
|SQL_DESC_DISPLAY_SIZE|Supported|  
|SQL_DESC_FIXED_PREC_SCALE|支持 (为 TRUE，money)|  
|SQL_DESC_INDICATOR_PTR|Supported|  
|SQL_DESC_LABEL|Supported|  
|SQL_DESC_LENGTH|Supported|  
|SQL_DESC_LITERAL_PREFIX|Supported|  
|SQL_DESC_LITERAL_SUFFIX|Supported|  
|SQL_DESC_LOCAL_TYPE_NAME|不支持 （返回空字符串）|  
|SQL_DESC_NAME|Supported|  
|SQL_DESC_NULLABLE|Supported<br /><br /> **请注意**前面 Jet 4.0 的版本中不受支持|  
|SQL_DESC_NUM_PREC_RADIX|Supported|  
|SQL_DESC_OCTET_LENGTH|Supported|  
|SQL_DESC_OCTET_LENGTH_PTR|Supported|  
|SQL_DESC_PARAMETER_TYPE|仅输入的参数|  
|SQL_DESC_PRECISION|Supported|  
|SQL_DESC_SCALE|Supported|  
|SQL_DESC_SCHEMA_NAME|不支持|  
|SQL_DESC_SEARCHABLE|Supported|  
|SQL_DESC_TABLE_NAME|不支持|  
|SQL_DESC_TYPE|Supported|  
|SQL_DESC_TYPE_NAME|Supported|  
|SQL_DESC_UNNAMED|Supported|  
|SQL_DESC_UNSIGNED|Supported|  
|SQL_DESC_UPDATABLE|Supported|
