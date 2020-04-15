---
title: 行为变化 |微软文档
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
ms.openlocfilehash: 3e4a433531d90eb0f89d9a5e446464b13fd02526
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283437"
---
# <a name="behavioral-changes"></a>行为更改
行为更改是*接口语法保持不变*但*语义*已更改的更改。 对于这些更改，ODBC 2 中使用的功能。*x*的行为方式与 ODBC 3 中的相同功能不同。*x*. .  
  
 应用程序是否展示 ODBC 2。*x*行为或 ODBC 3。*x*行为由SQL_ATTR_ODBC_VERSION环境属性决定。 此 32 位值设置为SQL_OV_ODBC2以显示 ODBC 2。*x*行为，并SQL_OV_ODBC3展示 ODBC 3。*x*行为。  
  
 SQL_ATTR_ODBC_VERSION环境属性由对**SQLSetEnvAttr**的调用设置。 在应用程序调用**SQLAllocHandle**来分配环境句柄后，它必须立即调用**SQLSetEnvAttr**来设置它显示的行为。 （因此，有一个新的环境状态来描述在已分配但无版本状态中的环境句柄。有关详细信息，请参阅附录[B：ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 应用程序会指出它与SQL_ATTR_ODBC_VERSION环境属性一起表现出的行为，但该属性对应用程序与 ODBC 2 的连接没有影响。*x*或 ODBC 3。*x*驱动程序。 ODBC 3.*x*应用程序可以连接到 ODBC 2。*x*或 3。*x*驱动程序，无论环境属性设置如何。  
  
 ODBC 3.*x*应用程序绝不应调用**SQLAllocEnv**。 因此，如果驱动程序管理器收到对**SQLAllocEnv**的调用，它将应用程序识别为 ODBC 2。*x*应用程序。  
  
 SQL_ATTR_ODBC_VERSION属性影响 ODBC 3 的三个不同方面。*x*驱动程序的行为：  
  
-   SQLSTATEs  
  
-   日期、时间和时间戳的数据类型  
  
-   **SQLTables**中的*目录名称*参数接受 ODBC 3 中的搜索模式。*x*，但不是在 ODBC 2 中。*x*  
  
 SQL_ATTR_ODBC_VERSION环境属性的设置不会影响**SQLSetParam**或**SQLBindParam**。 **SQLColAttribute**也不受此位的影响。 尽管**SQLColAttribute**返回受 ODBC 版本（日期类型、精度、比例和长度）影响的属性，但预期行为由*FieldIdentifier*参数的值决定。 当*字段标识符*等于SQL_DESC_TYPE时 **，SQLColAttribute**返回 ODBC 3。*x*日期、时间和时间戳的代码;当*字段标识符*等于SQL_COLUMN_TYPE时 **，SQLColAttribute**返回 ODBC 2。*x*日期、时间和时间戳的代码。  
  
 本部分包含以下主题。  
  
-   [SQLSTATE 映射](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Datetime 数据类型更改](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
