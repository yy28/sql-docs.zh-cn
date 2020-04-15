---
title: 属性一致性 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
- conformance levels [ODBC], attribute
- attribute conformance levels [ODBC]
ms.assetid: 34fea100-10f9-46d5-bc50-3aa867b70f24
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2880a35f4bdc997cc037cdd0d60720267ff4a58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306398"
---
# <a name="attribute-conformance"></a>属性一致性
下表指示每个 ODBC 环境属性的一致性级别，其中定义良好。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|核心|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] 这是一个可选功能，因此不是一致性级别的一部分。  
  
 下表指示每个 ODBC 连接属性的一致性级别，其中定义良好。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|核心|  
|SQL_ATTR_ASYNC_ENABLE|级别 1/级别 2[1]|  
|SQL_ATTR_AUTO_IPD|级别 2|  
|SQL_ATTR_AUTOCOMMIT|级别 1|  
|SQL_ATTR_CONNECTION_DEAD|级别 1|  
|SQL_ATTR_CONNECTION_TIMEOUT|级别 2|  
|SQL_ATTR_CURRENT_CATALOG|级别 2|  
|SQL_ATTR_LOGIN_TIMEOUT|级别 2|  
|SQL_ATTR_ODBC_CURSORS|核心|  
|SQL_ATTR_PACKET_SIZE|级别 2|  
|SQL_ATTR_QUIET_MODE|核心|  
|SQL_ATTR_TRACE|核心|  
|SQL_ATTR_TRACEFILE|核心|  
|SQL_ATTR_TRANSLATE_LIB|核心|  
|SQL_ATTR_TRANSLATE_OPTION|核心|  
|SQL_ATTR_TXN_ISOLATION|级别 1/级别 2[2]|  
  
 [1] 支持连接级异步（级别 1 需要）的应用程序必须支持通过调用**SQLSetConnectAttr**将此属性设置为SQL_TRUE;属性不必通过**SQLSetStmtAttr**将其默认值以外的值设置为该值。 支持语句级异步（级别 2 需要）的应用程序必须支持使用任一函数将此属性设置为SQL_TRUE。  
  
 [2] 对于级别 1 接口一致性，驱动程序除了支持驱动程序定义的默认值外还必须支持一个值（通过使用SQL_DEFAULT_TXN_ISOLATION选项调用**SQLGetInfo**可用）。 对于 2 级接口一致性，驱动程序还必须支持SQL_TXN_SERIALIZABLE。  
  
 下表指示每个 ODBC 语句属性的一致性级别，其中定义良好。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|核心|  
|SQL_ATTR_APP_ROW_DESC|核心|  
|SQL_ATTR_ASYNC_ENABLE|级别 1/级别 2[1]|  
|SQL_ATTR_CONCURRENCY|级别 1/级别 2[2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|级别 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|级别 2|  
|SQL_ATTR_CURSOR_TYPE|核心/级别 2[3]|  
|SQL_ATTR_ENABLE_AUTO_IPD|级别 2|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|级别 2|  
|SQL_ATTR_IMP_PARAM_DESC|核心|  
|SQL_ATTR_IMP_ROW_DESC|核心|  
|SQL_ATTR_KEYSET_SIZE|级别 2|  
|SQL_ATTR_MAX_LENGTH|级别 1|  
|SQL_ATTR_MAX_ROWS|级别 1|  
|SQL_ATTR_METADATA_ID|核心|  
|SQL_ATTR_NOSCAN|核心|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|核心|  
|SQL_ATTR_PARAM_BIND_TYPE|核心|  
|SQL_ATTR_PARAM_OPERATION_PTR|核心|  
|SQL_ATTR_PARAM_STATUS_PTR|核心|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|核心|  
|SQL_ATTR_PARAMSET_SIZE|核心|  
|SQL_ATTR_QUERY_TIMEOUT|级别 2|  
|SQL_ATTR_RETRIEVE_DATA|级别 1|  
|SQL_ATTR_ROW_ARRAY_SIZE|核心|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|核心|  
|SQL_ATTR_ROW_BIND_TYPE|核心|  
|SQL_ATTR_ROW_NUMBER|级别 1|  
|SQL_ATTR_ROW_OPERATION_PTR|级别 1|  
|SQL_ATTR_ROW_STATUS_PTR|核心|  
|SQL_ATTR_ROWS_FETCHED_PTR|核心|  
|SQL_ATTR_SIMULATE_CURSOR|级别 2|  
|SQL_ATTR_USE_BOOKMARKS|级别 2|  
  
 [1] 支持连接级异步（级别 1 需要）的应用程序必须支持通过调用**SQLSetConnectAttr**将此属性设置为SQL_TRUE;属性不必通过**SQLSetStmtAttr**将其默认值以外的值设置为该值。 支持语句级异步（级别 2 需要）的应用程序必须支持使用任一函数将此属性设置为SQL_TRUE。  
  
 [2] 对于 2 级接口一致性，驱动程序必须支持SQL_CONCUR_READ_ONLY和至少一个其他值。  
  
 [3] 对于 1 级接口一致性，驱动程序必须支持SQL_CURSOR_FORWARD_ONLY和至少一个其他值。 对于级别 2 接口一致性，驱动程序必须支持本文档中定义的所有值。
