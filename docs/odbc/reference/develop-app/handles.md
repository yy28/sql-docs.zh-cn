---
title: 处理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- handles [ODBC]
- driver handles [ODBC]
- driver manager [ODBC], handles
- handles [ODBC], about handles
ms.assetid: f663101e-a4cc-402b-b9d7-84d5e975be71
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a205a23c4c7e7e45269fd00fc0923d4168ec7091
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061436"
---
# <a name="handles"></a>控点
句柄是不透明的 32 位值，标识特定的项;在 ODBC 中，此项可以是环境、 连接、 语句或描述符。 当应用程序调用**SQLAllocHandle**、 驱动程序管理器或驱动程序创建指定类型的新项并返回其句柄到应用程序。 更高版本的应用程序使用该句柄来调用 ODBC 函数时标识该项。 驱动程序管理器和驱动程序使用该句柄来查找有关项目的信息。  
  
 例如，以下代码使用两个语句句柄 (*hstmtOrder*并*hstmtLine*) 来标识要在其中创建结果集的销售订单和销售订单行号的语句。 更高版本，它使用这些句柄来标识从中获取数据的结果集。  
  
```  
SQLHSTMT      hstmtOrder, hstmtLine; // Statement handles.  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
SQLRETURN     rc;  
  
// Prepare the statement that retrieves line number information.  
SQLPrepare(hstmtLine, "SELECT * FROM Lines WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter in the preceding statement.  
SQLBindParameter(hstmtLine, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
               &OrderID, 0, &OrderIDInd);  
  
// Bind the result sets for the Order table and the Lines table. Bind  
// OrderID to the OrderID column in the Orders table. When each row is  
// fetched, OrderID will contain the current order ID, which will then be  
// passed as a parameter to the statement tofetch line number  
// information. Code not shown.  
  
// Create a result set of sales orders.  
SQLExecDirect(hstmtOrder, "SELECT * FROM Orders", SQL_NTS);  
  
// Fetch and display the sales order data. Code to check if rc equals  
// SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmtOrder)) != SQL_NO_DATA) {  
   // Display the sales order data. Code not shown.  
  
   // Create a result set of line numbers for the current sales order.  
   SQLExecute(hstmtLine);  
  
   // Fetch and display the sales order line number data. Code to check  
   // if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLFetch(hstmtLine)) != SQL_NO_DATA) {  
      // Display the sales order line number data. Code not shown.  
   }  
  
   // Close the sales order line number result set.  
   SQLCloseCursor(hstmtLine);  
}  
  
// Close the sales order result set.  
SQLCloseCursor(hstmtOrder);  
```  
  
 句柄是仅对创建它们; ODBC 组件有意义也就是说，仅驱动程序管理器可以解释驱动程序管理器句柄和驱动程序仅可以解释其自己的句柄。  
  
 例如，假设在前面的示例驱动程序分配的结构来存储有关语句的信息，并返回指向此结构作为语句句柄的指针。 当应用程序调用**SQLPrepare**，则它将 SQL 语句，该语句的句柄用于销售订单行号。 该驱动程序将 SQL 语句发送到数据源，使其做好准备，并返回访问计划标识符。 驱动程序使用该句柄来查找要在其中存储此标识符的结构。  
  
 随后，当应用程序调用**SQLExecute**若要生成特定的销售订单的行号的结果集，它将传递相同的句柄。 驱动程序使用该句柄从结构检索访问计划标识符。 它将标识符发送到数据源，以告诉它要执行的计划。  
  
 ODBC 具有两个级别的句柄：驱动程序管理器句柄和驱动程序句柄。 应用程序调用 ODBC 函数，因为它在驱动程序管理器中调用这些函数时使用驱动程序管理器句柄。 驱动程序管理器使用此句柄来查找相应的驱动程序句柄，并驱动程序中调用函数时使用的驱动程序句柄。 有关如何使用驱动程序和驱动程序管理器句柄的示例，请参阅[的连接过程中的驱动程序管理器角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 有两个级别的句柄是 ODBC 体系结构; 的项目在大多数情况下，不相关的应用程序或驱动程序。 尽管通常没有任何理由这么做，但它是应用程序可以通过调用确定驱动程序句柄**SQLGetInfo**。  
  
 本部分包含以下主题。  
  
-   [环境句柄](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [连接句柄](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [语句句柄](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [描述符句柄](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [状态转换](../../../odbc/reference/develop-app/state-transitions.md)
