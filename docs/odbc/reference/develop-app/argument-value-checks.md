---
title: 参数值检查 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c6e4de16c4a1a80be893acbc7a1993b375f2fee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298816"
---
# <a name="argument-value-checks"></a>参数值检查
驱动程序管理器检查以下类型的参数。 除非另有说明，否则驱动程序管理器将返回SQL_ERROR参数值中的错误。  
  
-   环境、连接和语句句柄通常不能为空指针。 驱动程序管理器在找到空句柄时返回SQL_INVALID_HANDLE。  
  
-   所需的指针参数（如**SQLAllocHandle**中的*OutputHandlePtr*和**SQLSetCursorName**中的*CursorName）* 不能为空指针。  
  
-   不支持特定于驱动程序的值的选项标志必须是一个法定值。 例如 **，SQLSetPos**中的*操作*必须SQL_POSITION、SQL_REFRESH、SQL_UPDATE、SQL_DELETE或SQL_ADD。  
  
-   驱动程序支持的 ODBC 版本中必须支持选项标志。 例如，在调用 ODBC 2.0 驱动程序时，无法SQL_ASYNC_MODE **SQLGetInfo**中*的信息类型*（在 ODBC 3.0 中引入）。  
  
-   列和参数编号必须大于 0 或大于或等于 0，具体取决于函数。 驱动程序必须基于当前结果集或 SQL 语句检查这些参数值的上限。  
  
-   长度/指示器参数和数据缓冲区长度参数必须包含适当的值。 例如，在**SQLColumns** *（NameLength3）* 中指定表名长度的参数必须SQL_NTS或大于 0 的值;**SQLDescribeCol**中的*缓冲区长度*必须大于或等于 0。 驱动程序可能还需要检查这些参数。 例如，它可能会检查*NameLength3*小于或等于数据源中表名的最大长度。
