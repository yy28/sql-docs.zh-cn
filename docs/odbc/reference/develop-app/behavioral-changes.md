---
title: "行为更改 |Microsoft 文档"
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
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3941b8cdc2a53cb0f9fe3ad2b94f2ef972ad3775
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="behavioral-changes"></a>行为更改
行为的更改是，这些更改*语法*接口的保持不变，但*语义*已更改。 有关这些更改后，在 ODBC 2 中使用的功能。*x*不同 ODBC 3 中的相同功能的行为。*x*。  
  
 是否应用程序显示 ODBC 2。*x*行为或 ODBC 3。*x*行为由 SQL_ATTR_ODBC_VERSION 环境属性。 此 32 位值设置为 SQL_OV_ODBC2 展示 ODBC 2。*x*行为和 SQL_OV_ODBC3 展示 ODBC 3。*x*行为。  
  
 通过调用设置了 SQL_ATTR_ODBC_VERSION 环境属性**SQLSetEnvAttr**。 应用程序调用后**SQLAllocHandle**分配环境句柄，它必须调用**SQLSetEnvAttr**立即将它展示的行为。 （因此，没有为新环境状态来描述在已分配，但 versionless 的环境句柄的状态。）有关详细信息，请参阅[附录 b: ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 应用程序，指出哪些行为，它展示 SQL_ATTR_ODBC_VERSION 环境属性，但该属性不起与 ODBC 2 的应用程序的连接。*x*或 ODBC 3。*x*驱动程序。 一个 ODBC 3。*x*应用程序可以连接到 ODBC 2。*x*或 3。*x*驱动程序，无论 environment 属性的设置。  
  
 ODBC 3。*x*应用程序应永远不会调用**SQLAllocEnv**。 因此，如果驱动程序管理器时接收调用**SQLAllocEnv**，它可以识别 ODBC 2 形式的应用程序。*x*应用程序。  
  
 SQL_ATTR_ODBC_VERSION 特性影响 ODBC 3 的三个不同的方面。*x*驱动程序的行为：  
  
-   SQLSTATEs  
  
-   有关日期、 时间和时间戳数据类型  
  
-   *CatalogName*中的参数**SQLTables**接受 ODBC 3 中的搜索模式。*x*，但不是在 ODBC 2。*x*  
  
 SQL_ATTR_ODBC_VERSION 环境属性的设置不会影响**SQLSetParam**或**SQLBindParam**。 **SQLColAttribute**也不受此位。 尽管**SQLColAttribute**返回受影响的属性通过 ODBC （日期类型、 精度、 小数位数和长度） 的版本，预期的行为由的值*FieldIdentifier*自变量。 当*FieldIdentifier*等于 SQL_DESC_TYPE， **SQLColAttribute**返回 ODBC 3。*x*的日期、 时间和时间戳; 代码时*FieldIdentifier*等于 SQL_COLUMN_TYPE， **SQLColAttribute**返回 ODBC 2。*x*日期、 时间和时间戳的代码。  
  
 本部分包含以下主题。  
  
-   [SQLSTATE 映射](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Datetime 数据类型更改](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
