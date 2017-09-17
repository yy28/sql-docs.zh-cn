---
title: "启用跟踪 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d80f7e70915c11a3a45f90d2821b9c1bd137d9dd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="enabling-tracing"></a>启用跟踪
跟踪在可以启用以下三种方式：  
  
-   设置**跟踪**和**TraceFile** Odbc.ini 注册表项中的关键字。 这启用或禁用跟踪时**SQLAllocHandle**与*HandleType* SQL_HANDLE_ENV 的调用。 ODBC 数据源管理器中显示的对话框在数据源安装过程中的跟踪选项卡中设置这些选项。 有关详细信息，请参阅[数据源的注册表项](../../../odbc/reference/install/registry-entries-for-data-sources.md)。  
  
-   调用**SQLSetConnectAttr**将 SQL_ATTR_TRACE 连接属性设置为 SQL_OPT_TRACE_ON。 这将启用，或连接的持续时间内禁用跟踪。 有关详细信息，请参阅[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函数说明。  
  
-   使用**ODBCSharedTraceFlag**若要打开或关闭跟踪动态。 (有关详细信息，请参阅下一主题[动态跟踪](../../../odbc/reference/develop-app/dynamic-tracing.md)。)
