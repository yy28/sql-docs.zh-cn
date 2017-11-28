---
title: "属性的一致性 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
- conformance levels [ODBC], attribute
- attribute conformance levels [ODBC]
ms.assetid: 34fea100-10f9-46d5-bc50-3aa867b70f24
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7859fbb5483acd09dd99f4f27be77d5874e7b992
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="attribute-conformance"></a>属性的一致性
下表指示这是定义完善的每个 ODBC 环境属性，一致性级别。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|核心|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] 这是一项可选功能，这种情况下不是一致性级别的一部分。  
  
 下表指示这是定义完善的每个 ODBC 连接属性，一致性级别。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|核心|  
|SQL_ATTR_ASYNC_ENABLE|级别 1/级别 2 [1]|  
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
|SQL_ATTR_TXN_ISOLATION|级别 1/级别 2 [2]|  
  
 [1] 应用程序支持连接级别异步 （需要级别 1） 必须支持通过调用此属性设置为 SQL_TRUE **SQLSetConnectAttr**; 不需要为其默认值以外的值可设置属性通过值**SQLSetStmtAttr**。 支持语句级异步 （需要级别 2） 的应用程序必须支持此属性设置为 SQL_TRUE 使用任一函数。  
  
 [2] 的第 1 级接口一致性的工具，该驱动程序必须支持除了驱动程序定义的默认值的一个值 (可通过调用**SQLGetInfo** SQL_DEFAULT_TXN_ISOLATION 选项)。 级别 2 接口符合规则，该驱动程序还必须支持 SQL_TXN_SERIALIZABLE。  
  
 下表指示这是定义完善的每个 ODBC 语句属性，一致性级别。  
  
|函数|一致性级别|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|核心|  
|SQL_ATTR_APP_ROW_DESC|核心|  
|SQL_ATTR_ASYNC_ENABLE|级别 1/级别 2 [1]|  
|SQL_ATTR_CONCURRENCY|级别 1/级别 2 [2]|  
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
  
 [1] 应用程序支持连接级别异步 （需要级别 1） 必须支持通过调用此属性设置为 SQL_TRUE **SQLSetConnectAttr**; 不需要为其默认值以外的值可设置属性通过值**SQLSetStmtAttr**。 支持语句级异步 （需要级别 2） 的应用程序必须支持此属性设置为 SQL_TRUE 使用任一函数。  
  
 [2] 的第 2 级接口一致性的工具，该驱动程序必须支持 SQL_CONCUR_READ_ONLY 和至少一个其他值。  
  
 [3] 的第 1 级接口一致性的工具，该驱动程序必须支持 SQL_CURSOR_FORWARD_ONLY 和至少一个其他值。 为级别 2 接口一致性，驱动程序必须支持本文档中定义的所有值。
