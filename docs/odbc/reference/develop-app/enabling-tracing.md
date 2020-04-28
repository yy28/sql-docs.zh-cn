---
title: 启用跟踪 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80bd4023a0260b67d11d7b4ded1bb810b81e0ab2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287347"
---
# <a name="enabling-tracing"></a>启用跟踪
可以通过以下三种方式启用跟踪：  
  
-   在 TraceFile 注册表项中设置**Trace**和**TraceFile**关键字。 如果调用**SQLAllocHandle**的 SQL_HANDLE_ENV *HandleType* ，则会启用或禁用跟踪。 这些选项是在数据源设置期间显示的 "ODBC 数据源管理器" 对话框的 "跟踪" 选项卡中设置的。 有关详细信息，请参阅[数据源的注册表项](../../../odbc/reference/install/registry-entries-for-data-sources.md)。  
  
-   调用**SQLSetConnectAttr** ，将 SQL_ATTR_TRACE 连接属性设置为 SQL_OPT_TRACE_ON。 这会在连接期间启用或禁用跟踪。 有关详细信息，请参阅[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函数说明。  
  
-   使用**ODBCSharedTraceFlag**动态启用或禁用跟踪。 （有关详细信息，请参阅下一主题[动态跟踪](../../../odbc/reference/develop-app/dynamic-tracing.md)。）
