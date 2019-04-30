---
title: 行为更改 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: abe670570dd2219247da0c70b2b62e1de4e60341
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181764"
---
# <a name="behavioral-changes"></a>行为更改
行为更改是为其这些更改*语法*接口的保持不变，但*语义*已更改。 有关这些更改，在 ODBC 2 中使用的功能。*x*行为将不同于在 ODBC 3 相同的功能。*x*。  
  
 无论应用程序表现出 ODBC 2。*x*行为或 ODBC 3。*x*行为由 SQL_ATTR_ODBC_VERSION 环境属性。 此 32 位值设置为 SQL_OV_ODBC2 展现出 ODBC 2。*x*行为和 SQL_OV_ODBC3 展现出 ODBC 3。*x*行为。  
  
 通过调用设置 SQL_ATTR_ODBC_VERSION 环境属性**SQLSetEnvAttr**。 应用程序调用后**SQLAllocHandle**若要在分配环境句柄，它必须调用**SQLSetEnvAttr**立即将它展示的行为。 （因此，没有为新环境状态来描述环境句柄在一个已分配但 versionless 的状态。）有关详细信息，请参阅[附录 b:状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 应用程序指出它展示 SQL_ATTR_ODBC_VERSION 环境属性，但该属性使用哪种行为上与 ODBC 2 应用程序的连接无效。*x*或 ODBC 3。*x*驱动程序。 ODBC 3。*x*应用程序可以连接到 ODBC 2。*x*或 3。*x*驱动程序，无论环境属性的设置。  
  
 ODBC 3。*x*应用程序应永远不会调用**SQLAllocEnv**。 因此，如果驱动程序管理器接收到调用**SQLAllocEnv**，它可以识别应用程序作为 ODBC 2。*x*应用程序。  
  
 SQL_ATTR_ODBC_VERSION 特性会影响 ODBC 3 的三个不同的方面。*x*驱动程序的行为：  
  
-   SQLSTATEs  
  
-   日期、 时间和时间戳的数据类型  
  
-   *CatalogName*中的参数**SQLTables**接受 ODBC 3 中的搜索模式。*x*，但不是在 ODBC 2。*x*  
  
 SQL_ATTR_ODBC_VERSION 环境属性的设置不会影响**SQLSetParam**或**SQLBindParam**。 **SQLColAttribute**也不受此位。 尽管**SQLColAttribute**返回受影响的属性的预期的行为由 ODBC （日期类型、 精度、 小数位数和长度） 的版本，由的值*FieldIdentifier*自变量。 当*FieldIdentifier*等于的 SQL_DESC_TYPE、 **SQLColAttribute**返回 ODBC 3。*x*的日期、 时间和时间戳; 代码时*FieldIdentifier*等于 SQL_COLUMN_TYPE， **SQLColAttribute**返回的 ODBC 2。*x*日期、 时间和时间戳的代码。  
  
 本部分包含以下主题。  
  
-   [SQLSTATE 映射](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Datetime 数据类型更改](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
