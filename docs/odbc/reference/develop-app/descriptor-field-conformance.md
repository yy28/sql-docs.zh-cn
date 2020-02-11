---
title: 描述符字段一致性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptor field conformance levels [ODBC]
- conformance levels [ODBC], descriptor field
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 6c29d93b-696c-4960-bff3-4d6bc41bc513
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afdb1f18ad641224d13373436dd58f1919a3d280
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67952348"
---
# <a name="descriptor-field-conformance"></a>描述符字段一致性
下表指明了每个 ODBC 描述符标头字段的一致性级别，其中定义正确。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|核心|  
|SQL_DESC_ARRAY_SIZE|核心|  
|SQL_DESC_ARRAY_STATUS_PTR|Core （适用于 APD、IPR 和 IRD）;级别1（适用于 ARD）|  
|SQL_DESC_BIND_OFFSET_PTR|核心|  
|SQL_DESC_BIND_TYPE|核心|  
|SQL_DESC_COUNT|核心|  
|SQL_DESC_ROWS_PROCESSED_PTR|核心|  
  
 下表指示每个 "ODBC 描述符记录" 字段的一致性级别，其中定义正确。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|级别 2|  
|SQL_DESC_BASE_COLUMN_NAME|核心|  
|SQL_DESC_BASE_TABLE_NAME|级别 1|  
|SQL_DESC_CASE_SENSITIVE|核心|  
|SQL_DESC_CATALOG_NAME|级别 2|  
|SQL_DESC_CONCISE_TYPE|核心|  
|SQL_DESC_DATA_PTR|核心|  
|SQL_DESC_DATETIME_INTERVAL_ 代码|Core [1]|  
|SQL_DESC_DATETIME_INTERVAL_ 精度|Core [1]|  
|SQL_DESC_DISPLAY_SIZE|核心|  
|SQL_DESC_FIXED_PREC_SCALE|核心|  
|SQL_DESC_INDICATOR_PTR|核心|  
|SQL_DESC_LABEL|级别 2|  
|SQL_DESC_LENGTH|核心|  
|SQL_DESC_LITERAL_PREFIX|核心|  
|SQL_DESC_LITERAL_SUFFIX|核心|  
|SQL_DESC_LOCAL_TYPE_NAME|核心|  
|SQL_DESC_NAME|核心|  
|SQL_DESC_NULLABLE|核心|  
|SQL_DESC_OCTET_LENGTH|核心|  
|SQL_DESC_OCTET_LENGTH_PTR|核心|  
|SQL_DESC_PARAMETER_TYPE|核心/级别 2 [2]|  
|SQL_DESC_PRECISION|核心|  
|SQL_DESC_ROWVER|级别 1|  
|SQL_DESC_SCALE|核心|  
|SQL_DESC_SCHEMA_NAME|级别 1|  
|SQL_DESC_SEARCHABLE|核心|  
|SQL_DESC_TABLE_NAME|级别 1|  
|SQL_DESC_TYPE|核心|  
|SQL_DESC_TYPE_NAME|核心|  
|SQL_DESC_UNNAMED|核心|  
|SQL_DESC_UNSIGNED|核心|  
|SQL_DESC_UPDATABLE|核心|  
  
 [1] 仅当驱动程序支持适用的数据类型时，才需要支持这些记录字段。  
  
 [2] 对于核心级一致性，驱动程序必须支持 SQL_PARAM_INPUT。 对于级别2接口一致性，驱动程序还必须支持 SQL_PARAM_INPUT_OUTPUT 和 SQL_PARAM_OUTPUT。
