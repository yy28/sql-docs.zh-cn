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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0096dad8fbb4cf9847385759702e39ac074c4c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112052"
---
# <a name="descriptors-and-desktop-database-drivers"></a>描述符和桌面数据库驱动程序
描述符是一个包含有关列数据或动态参数的信息的数据结构。 **SQLGetDescField**可用于检索下面列出的受支持的描述符。 不能因为自动填充实现参数描述符 (IPD) **SQLDescribeParam**不受支持。 不能通过 Jet （如 SQL_DESC_BASE_TABLE_NAME) 的描述符字段也不支持。  
  
 有关支持 Jet 的描述符字段的详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。  
  
 有关描述符的详细信息，请参阅"描述符"下的主题中*ODBC 程序员参考*。  
  
|描述符字段|支持级别|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|支持|  
|SQL_DESC_ARRAY_SIZE|仅支持 ARD|  
|SQL_DESC_ARRAY_STATUS_PTR|支持|  
|SQL_DESC_BIND_OFFSET_PTR|支持|  
|SQL_DESC_BIND_TYPE|支持|  
|SQL_DESC_COUNT|支持|  
|SQL_DESC_ROWS_PROCESSED_PTR|仅支持 ARD|  
|SQL_DESC_AUTO_UNIQUE_VALUE|支持|  
|SQL_DESC_BASE_COLUMN_NAME|支持 （新增）|  
|SQL_DESC_BASE_TABLE_NAME|支持 （新增）|  
|SQL_DESC_CASE_SENSITIVE|始终为 FALSE|  
|SQL_DESC_CATALOG_NAME|不支持|  
|SQL_DESC_CONCISE_TYPE|支持|  
|SQL_DESC_DATA_PTR|支持|  
|SQL_DESC_DATETIME_INTERVAL_CODE|支持|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|间隔 C 类型支持|  
|SQL_DESC_DISPLAY_SIZE|支持|  
|SQL_DESC_FIXED_PREC_SCALE|支持 (为 TRUE，资金)|  
|SQL_DESC_INDICATOR_PTR|支持|  
|SQL_DESC_LABEL|支持|  
|SQL_DESC_LENGTH|支持|  
|SQL_DESC_LITERAL_PREFIX|支持|  
|SQL_DESC_LITERAL_SUFFIX|支持|  
|SQL_DESC_LOCAL_TYPE_NAME|不支持 （返回空字符串）|  
|SQL_DESC_NAME|支持|  
|SQL_DESC_NULLABLE|支持<br /><br /> **请注意**Jet 4.0 之前的版本中不受支持|  
|SQL_DESC_NUM_PREC_RADIX|支持|  
|SQL_DESC_OCTET_LENGTH|支持|  
|SQL_DESC_OCTET_LENGTH_PTR|支持|  
|SQL_DESC_PARAMETER_TYPE|仅输入的参数|  
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
