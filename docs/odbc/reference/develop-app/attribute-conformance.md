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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71f0da7bbd7ef1a37a1f48539c7230bff0ceda15
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909916"
---
# <a name="attribute-conformance"></a>属性一致性
下表指示这是定义完善的一致性级别的每个 ODBC 环境属性。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|Core|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] 这是一项可选功能，这种情况下不是一致性级别的一部分。  
  
 下表指示这是定义完善的一致性级别的每个 ODBC 连接属性。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|Core|  
|SQL_ATTR_ASYNC_ENABLE|级别 1/级别 2 [1]|  
|SQL_ATTR_AUTO_IPD|级别 2|  
|SQL_ATTR_AUTOCOMMIT|级别 1|  
|SQL_ATTR_CONNECTION_DEAD|级别 1|  
|SQL_ATTR_CONNECTION_TIMEOUT|级别 2|  
|SQL_ATTR_CURRENT_CATALOG|级别 2|  
|SQL_ATTR_LOGIN_TIMEOUT|级别 2|  
|SQL_ATTR_ODBC_CURSORS|Core|  
|SQL_ATTR_PACKET_SIZE|级别 2|  
|SQL_ATTR_QUIET_MODE|Core|  
|SQL_ATTR_TRACE|Core|  
|SQL_ATTR_TRACEFILE|Core|  
|SQL_ATTR_TRANSLATE_LIB|Core|  
|SQL_ATTR_TRANSLATE_OPTION|Core|  
|SQL_ATTR_TXN_ISOLATION|级别 1/级别 2 [2]|  
  
 [1] 的应用程序支持连接级别异步 （需要级别 1） 必须支持通过调用此属性设置为 SQL_TRUE **SQLSetConnectAttr**; 属性不需要为其默认值以外的值可设置值通过**SQLSetStmtAttr**。 支持 （需要级别 2） 的语句级异步功能的应用程序必须支持此属性设置为 SQL_TRUE 使用这两种函数。  
  
 [2] 的级别 1 接口一致性的驱动程序必须支持除了驱动程序定义的默认值的一个值 (可通过调用**SQLGetInfo** SQL_DEFAULT_TXN_ISOLATION 选项)。 级别 2 接口一致性，驱动程序还必须支持 SQL_TXN_SERIALIZABLE。  
  
 下表指示这是定义完善的一致性级别的每个 ODBC 语句属性。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|Core|  
|SQL_ATTR_APP_ROW_DESC|Core|  
|SQL_ATTR_ASYNC_ENABLE|级别 1/级别 2 [1]|  
|SQL_ATTR_CONCURRENCY|级别 1/级别 2 [2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|级别 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|级别 2|  
|SQL_ATTR_CURSOR_TYPE|核心/级别 2 [3]|  
|SQL_ATTR_ENABLE_AUTO_IPD|级别 2|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|级别 2|  
|SQL_ATTR_IMP_PARAM_DESC|Core|  
|SQL_ATTR_IMP_ROW_DESC|Core|  
|SQL_ATTR_KEYSET_SIZE|级别 2|  
|SQL_ATTR_MAX_LENGTH|级别 1|  
|SQL_ATTR_MAX_ROWS|级别 1|  
|SQL_ATTR_METADATA_ID|Core|  
|SQL_ATTR_NOSCAN|Core|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|Core|  
|SQL_ATTR_PARAM_BIND_TYPE|Core|  
|SQL_ATTR_PARAM_OPERATION_PTR|Core|  
|SQL_ATTR_PARAM_STATUS_PTR|Core|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|Core|  
|SQL_ATTR_PARAMSET_SIZE|Core|  
|SQL_ATTR_QUERY_TIMEOUT|级别 2|  
|SQL_ATTR_RETRIEVE_DATA|级别 1|  
|SQL_ATTR_ROW_ARRAY_SIZE|Core|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|Core|  
|SQL_ATTR_ROW_BIND_TYPE|Core|  
|SQL_ATTR_ROW_NUMBER|级别 1|  
|SQL_ATTR_ROW_OPERATION_PTR|级别 1|  
|SQL_ATTR_ROW_STATUS_PTR|Core|  
|SQL_ATTR_ROWS_FETCHED_PTR|Core|  
|SQL_ATTR_SIMULATE_CURSOR|级别 2|  
|SQL_ATTR_USE_BOOKMARKS|级别 2|  
  
 [1] 的应用程序支持连接级别异步 （需要级别 1） 必须支持通过调用此属性设置为 SQL_TRUE **SQLSetConnectAttr**; 属性不需要为其默认值以外的值可设置值通过**SQLSetStmtAttr**。 支持 （需要级别 2） 的语句级异步功能的应用程序必须支持此属性设置为 SQL_TRUE 使用这两种函数。  
  
 [2] 为级别 2 接口一致性，驱动程序必须支持 SQL_CONCUR_READ_ONLY 和至少一个其他值。  
  
 [3] 的级别 1 接口一致性，驱动程序必须支持 SQL_CURSOR_FORWARD_ONLY 和至少一个其他值。 级别 2 接口一致性，驱动程序必须支持本文档中定义的所有值。
