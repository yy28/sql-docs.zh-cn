---
title: 描述符和桌面数据库驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ef79855f71d23e5a884822371f1894eb83442a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303508"
---
# <a name="descriptors-and-desktop-database-drivers"></a>描述符和桌面数据库驱动程序
描述符是保存有关列数据或动态参数的信息的数据结构。 **SQLGetDescField**可用于检索下面列出的支持的描述符。 由于不支持**SQLDescribeParam** ，因此不会自动填充实现参数描述符（IPD）。 也不支持不通过 Jet （如 SQL_DESC_BASE_TABLE_NAME）提供的描述符字段。  
  
 有关 Jet 支持的描述符字段的详细信息，请参阅*Microsoft jet 数据库引擎程序员指南*。  
  
 有关描述符的详细信息，请参阅*ODBC 程序员参考*中的 "描述符" 下的主题。  
  
|描述符字段|支持级别|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|支持|  
|SQL_DESC_ARRAY_SIZE|仅 ARD 支持|  
|SQL_DESC_ARRAY_STATUS_PTR|支持|  
|SQL_DESC_BIND_OFFSET_PTR|支持|  
|SQL_DESC_BIND_TYPE|支持|  
|SQL_DESC_COUNT|支持|  
|SQL_DESC_ROWS_PROCESSED_PTR|仅 ARD 支持|  
|SQL_DESC_AUTO_UNIQUE_VALUE|支持|  
|SQL_DESC_BASE_COLUMN_NAME|支持（新）|  
|SQL_DESC_BASE_TABLE_NAME|支持（新）|  
|SQL_DESC_CASE_SENSITIVE|始终为 FALSE|  
|SQL_DESC_CATALOG_NAME|不支持|  
|SQL_DESC_CONCISE_TYPE|支持|  
|SQL_DESC_DATA_PTR|支持|  
|SQL_DESC_DATETIME_INTERVAL_CODE|支持|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|支持的时间间隔 C 类型|  
|SQL_DESC_DISPLAY_SIZE|支持|  
|SQL_DESC_FIXED_PREC_SCALE|支持（适用于 money）|  
|SQL_DESC_INDICATOR_PTR|支持|  
|SQL_DESC_LABEL|支持|  
|SQL_DESC_LENGTH|支持|  
|SQL_DESC_LITERAL_PREFIX|支持|  
|SQL_DESC_LITERAL_SUFFIX|支持|  
|SQL_DESC_LOCAL_TYPE_NAME|不支持（返回空字符串）|  
|SQL_DESC_NAME|支持|  
|SQL_DESC_NULLABLE|支持<br /><br /> **注意**在 Jet 4.0 以前的版本中不受支持|  
|SQL_DESC_NUM_PREC_RADIX|支持|  
|SQL_DESC_OCTET_LENGTH|支持|  
|SQL_DESC_OCTET_LENGTH_PTR|支持|  
|SQL_DESC_PARAMETER_TYPE|仅输入参数|  
|SQL_DESC_PRECISION|支持|  
|SQL_DESC_SCALE|支持|  
|SQL_DESC_SCHEMA_NAME|不支持|  
|SQL_DESC_SEARCHABLE|支持|  
|SQL_DESC_TABLE_NAME|不支持|  
|SQL_DESC_TYPE|支持|  
|SQL_DESC_TYPE_NAME|支持|  
|SQL_DESC_UNNAMED|支持|  
|SQL_DESC_UNSIGNED|支持|  
|SQL_DESC_UPDATABLE|支持|
