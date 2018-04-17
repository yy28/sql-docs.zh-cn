---
title: 自变量值检查 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8b3e4c8772a8d6a6b2a00f6c8ffe4ab610d0e1ec
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="argument-value-checks"></a>自变量值检查
驱动程序管理器检查以下类型的自变量。 除非另行说明，否则驱动程序管理器将返回 SQL_ERROR 自变量值中的错误。  
  
-   通常，环境、 连接和语句的句柄不能为 null 指针。 找到句柄为空时，驱动程序管理器将返回 SQL_INVALID_HANDLE。  
  
-   需要指针自变量，如*OutputHandlePtr*中**SQLAllocHandle**和*CursorName*中**SQLSetCursorName**，不能为null 指针。  
  
-   不支持特定于驱动程序的值的选项标志必须是一个合法值。 例如，*操作*中**SQLSetPos** SQL_POSITION、 SQL_REFRESH、 SQL_UPDATE、 SQL_DELETE 或 SQL_ADD 必须。  
  
-   中的 ODBC 驱动程序支持的版本必须支持选项标志。 例如，*信息类型*中**SQLGetInfo**不能为 SQL_ASYNC_MODE （在 ODBC 3.0 中引入） 时调用的 ODBC 2.0 的驱动程序。  
  
-   列和参数号必须大于 0 或大于或等于 0，具体取决于该函数。 驱动程序必须检查这些基于当前结果集或 SQL 语句的参数值的上限。  
  
-   长度/指示器参数和数据缓冲区的长度参数必须包含适当的值。 例如，自变量指定中的表名的长度**SQLColumns** (*NameLength3*) 必须是 sql_nts 以或值大于 0;*BufferLength*中**SQLDescribeCol**必须大于或等于 0。 该驱动程序可能还需要检查这些自变量。 例如，它可能会检查*NameLength3*小于或等于数据源中的表名称的最大长度。
