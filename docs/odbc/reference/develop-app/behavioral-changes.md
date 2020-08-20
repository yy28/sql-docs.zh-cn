---
description: 行为更改
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6fb5501d362cb46f3616e58c5a4994bab86e00ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461619"
---
# <a name="behavioral-changes"></a>行为更改
行为更改是指这些更改，接口的 *语法* 保持不变，但 *语义* 发生了更改。 对于这些更改，为 ODBC 2 中使用的功能。*x* 的行为不同于 ODBC 3 中的相同功能。*x*。  
  
 应用程序是否展示 ODBC 2。*x* 行为或 ODBC 3。*x* 行为取决于 SQL_ATTR_ODBC_VERSION 环境属性。 此32位值设置为显示 ODBC 2 SQL_OV_ODBC2。*x* 行为，并 SQL_OV_ODBC3 展示 ODBC 3。*x* 行为。  
  
 SQL_ATTR_ODBC_VERSION 环境特性是通过调用 **SQLSetEnvAttr**设置的。 在应用程序调用 **SQLAllocHandle** 来分配环境句柄之后，必须立即调用**SQLSetEnvAttr** 来设置它所展示的行为。  (因此，有一个新的环境状态用于在已分配但 versionless 的状态下描述环境句柄。 ) 有关详细信息，请参阅 [附录 B： ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 应用程序规定它与 SQL_ATTR_ODBC_VERSION 环境属性表现的行为，但该属性对应用程序与 ODBC 2 的连接不起作用。*x* 或 ODBC 3。*x* 驱动程序。 ODBC 3。*x* 应用程序可以连接到 ODBC 2。*x* 或3。*x* 驱动程序，不管环境属性的设置如何。  
  
 ODBC 3。*x* 应用程序不应调用 **SQLAllocEnv**。 因此，如果驱动程序管理器接收到对 **SQLAllocEnv**的调用，它会将该应用程序识别为 ODBC 2。*x* 应用程序。  
  
 SQL_ATTR_ODBC_VERSION 特性会影响 ODBC 3 的三个不同方面。*x* 驱动程序的行为：  
  
-   SQLSTATEs  
  
-   日期、时间和时间戳的数据类型  
  
-   **SQLTables**中的*CATALOGNAME*参数接受 ODBC 3 中的搜索模式。*x*，但不在 ODBC 2 中。*x*  
  
 SQL_ATTR_ODBC_VERSION 环境属性的设置不会影响 **SQLSetParam** 或 **SQLBindParam**。 **SQLColAttribute** 也不受此位的影响。 尽管 **SQLColAttribute** 返回受 ODBC 版本 (日期类型、精度、小数位数和长度) 影响的属性，但预期的行为由 *FieldIdentifier* 参数的值确定。 当 *FieldIdentifier* 等于 SQL_DESC_TYPE 时， **SQLCOLATTRIBUTE** 将返回 ODBC 3。日期、时间和时间戳的*x* 代码;当 *FieldIdentifier* 等于 SQL_COLUMN_TYPE 时， **SQLCOLATTRIBUTE** 将返回 ODBC 2。日期、时间和时间戳的*x* 代码。  
  
 本部分包含以下主题。  
  
-   [SQLSTATE 映射](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Datetime 数据类型更改](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
