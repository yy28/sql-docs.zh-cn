---
title: 参数值检查 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dfee0dd00e30f6446430156617ba45a5a39b994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288553"
---
# <a name="argument-value-checks"></a>参数值检查
驱动程序管理器检查以下类型的参数。 除非另有说明，驱动程序管理器中的参数值的错误返回 SQL_ERROR。  
  
-   环境、 连接和语句句柄通常不能为 null 指针。 驱动程序管理器返回 SQL_INVALID_HANDLE 时查找句柄为空。  
  
-   所需的指针参数，如*OutputHandlePtr*中**SQLAllocHandle**并*CursorName*中**SQLSetCursorName**，不能为null 指针。  
  
-   不支持特定于驱动程序的值的选项标记必须是合法的值。 例如，*操作*中**SQLSetPos** SQL_POSITION、 SQL_REFRESH、 SQL_UPDATE、 SQL_DELETE 或 SQL_ADD 必须。  
  
-   必须在 ODBC 驱动程序支持的版本中支持选项标志。 例如，*信息类型*中**SQLGetInfo**不能为 SQL_ASYNC_MODE （在 ODBC 3.0 中引入） 时调用 ODBC 2.0 驱动程序。  
  
-   列和参数号必须大于 0 或大于或等于 0，具体取决于该函数。 该驱动程序必须检查这些基于当前结果集或 SQL 语句的参数值的上限。  
  
-   长度/指示器参数和数据缓冲区长度参数必须包含相应的值。 例如，指定的表名中的长度的参数**SQLColumns** (*NameLength3*) 必须为 SQL_NTS 或值大于 0;*BufferLength*中**SQLDescribeCol**必须大于或等于 0。 该驱动程序可能还需要检查这些参数。 例如，它可能会检查*NameLength3*小于或等于的表名中的数据源的最大长度。
