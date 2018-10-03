---
title: 如何实现游标 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC], about ODBC cursors
ms.assetid: 2b1d7dd4-08a4-43fc-b3eb-70c183d0941f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c92391b1d8874da3a8901ccc5c6245e48334241
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155710"
---
# <a name="how-cursors-are-implemented"></a>如何实现游标
  ODBC 应用程序通过在执行 SQL 语句之前设置一个或多个语句属性来控制游标的行为。 ODBC 采用以下两种不同方式来指定游标的特征：  
  
-   游标类型  
  
     使用的 SQL_ATTR_CURSOR_TYPE 属性来设置游标类型[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)。 ODBC 游标类型包括只进、静态、由键集驱动、混合和动态。 设置游标类型是在 ODBC 中指定游标的原始方法。  
  
-   游标行为  
  
     使用 SQL_ATTR_CURSOR_SCROLLABLE 和 SQL_ATTR_CURSOR_SENSITIVITY 属性的设置游标行为**SQLSetStmtAttr**。 这些属性根据在 ISO 标准中为 DECLARE CURSOR 语句定义的 SCROLL 和 SENSITIVE 关键字建模。 这两个 ISO 选项是在 ODBC 版本 3.0 中引入的。  
  
 应使用上述两种方法之一指定 ODBC 游标的特征，首选方法为使用 ODBC 游标类型。  
  
 除设置游标类型以外，ODBC 应用程序还会设置其他选项，例如每次提取返回的行数、并发选项和事务隔离级别。 可以针对 ODBC 样式的游标（只进、静态、由键集驱动、混合和动态）或 ISO 样式的游标（可滚动性和敏感性）设置这些选项。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持多种以物理方式实现各种类型的游标。 该驱动程序使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 默认结果集实现某些类型的游标，并将其他类型的游标作为服务器游标或使用 ODBC 游标库实现。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [使用 SQL Server 默认结果集](using-sql-server-default-result-sets.md)  
  
-   [使用服务器游标](using-server-cursors.md)  
  
-   [ODBC 游标库](odbc-cursor-library.md)  
  
## <a name="see-also"></a>请参阅  
 [使用游标&#40;ODBC&#41;](../using-cursors-odbc.md)  
  
  
