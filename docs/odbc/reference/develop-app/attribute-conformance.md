---
title: 属性一致性 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306398"
---
# <a name="attribute-conformance"></a>属性一致性
下表指明了每个 ODBC 环境属性的一致性级别，其中定义正确。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|核心|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] 这是一项可选功能，因此不属于一致性级别。  
  
 下表指明了每个 ODBC 连接属性的一致性级别，其中定义正确。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|核心|  
|SQL_ATTR_ASYNC_ENABLE|第1级/第2级 [1]|  
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
|SQL_ATTR_TXN_ISOLATION|第1级/第2级 [2]|  
  
 [1] 支持连接级别的异步的应用程序（级别1需要）必须支持通过调用**SQLSetConnectAttr**将此特性设置为 SQL_TRUE;不需要通过**SQLSetStmtAttr**将该属性设置为其默认值以外的值。 支持语句级别的异步的应用程序（级别2需要）必须支持使用任一函数将此特性设置为 SQL_TRUE。  
  
 [2] 对于级别1接口一致性，驱动程序必须支持一个值以及驱动程序定义的默认值（可通过使用 SQL_DEFAULT_TXN_ISOLATION 选项调用**SQLGetInfo**来访问）。 对于级别2接口一致性，驱动程序还必须支持 SQL_TXN_SERIALIZABLE。  
  
 下表指示每个 ODBC 语句属性的一致性级别，其中定义正确。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|核心|  
|SQL_ATTR_APP_ROW_DESC|核心|  
|SQL_ATTR_ASYNC_ENABLE|第1级/第2级 [1]|  
|SQL_ATTR_CONCURRENCY|第1级/第2级 [2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|级别 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|级别 2|  
|SQL_ATTR_CURSOR_TYPE|核心/级别 2 [3]|  
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
  
 [1] 支持连接级别的异步的应用程序（级别1需要）必须支持通过调用**SQLSetConnectAttr**将此特性设置为 SQL_TRUE;不需要通过**SQLSetStmtAttr**将该属性设置为其默认值以外的值。 支持语句级别的异步的应用程序（级别2需要）必须支持使用任一函数将此特性设置为 SQL_TRUE。  
  
 [2] 对于级别2接口一致性，驱动程序必须支持 SQL_CONCUR_READ_ONLY 和至少一个其他值。  
  
 [3] 对于级别1接口一致性，驱动程序必须支持 SQL_CURSOR_FORWARD_ONLY 和至少一个其他值。 对于级别2接口一致性，驱动程序必须支持本文档中定义的所有值。
