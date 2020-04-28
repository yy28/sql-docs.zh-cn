---
title: Handles |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 713c2a71ec195b75d682b97239413e98d07b5861
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300207"
---
# <a name="handles"></a>控点
句柄是用于标识特定项的不透明、32位的值;在 ODBC 中，此项可以是环境、连接、语句或描述符。 当应用程序调用**SQLAllocHandle**时，驱动程序管理器或驱动程序将创建指定类型的新项，并将其句柄返回到应用程序。 稍后，应用程序使用该句柄在调用 ODBC 函数时标识该项。 驱动程序管理器和驱动程序使用该句柄来查找有关项的信息。  
  
 例如，以下代码使用两个语句句柄（*hstmtOrder*和*hstmtLine*）来标识要在其上创建销售订单和销售订单行号的结果集的语句。 稍后将使用这些句柄来确定要从中提取数据的结果集。  
  
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
  
 句柄仅对创建它们的 ODBC 组件有意义;也就是说，只有驱动程序管理器可以解释驱动程序管理器句柄，而只有驱动程序可以解释它自己的句柄。  
  
 例如，假设上一示例中的驱动程序分配了一个结构来存储有关语句的信息，并将该指针作为语句句柄返回到此结构中。 当应用程序调用**SQLPrepare**时，它将传递 SQL 语句和用于销售订单行号的语句的句柄。 驱动程序将 SQL 语句发送到数据源，该语句将准备该语句并返回访问计划标识符。 驱动程序使用该句柄查找要在其中存储此标识符的结构。  
  
 稍后，当应用程序调用**SQLExecute**为特定销售订单生成行号的结果集时，它将传递相同的句柄。 驱动程序使用该句柄从结构中检索访问计划标识符。 它将标识符发送到数据源，告诉它要执行的计划。  
  
 ODBC 有两个级别的句柄：驱动程序管理器处理程序和驱动程序句柄。 应用程序在调用 ODBC 函数时使用驱动程序管理器句柄，因为它在驱动程序管理器中调用这些函数。 驱动程序管理器使用此句柄来查找相应的驱动程序句柄，并在调用驱动程序中的函数时使用驱动程序句柄。 有关如何使用驱动程序和驱动程序管理器处理程序的示例，请参阅[连接过程中的驱动程序管理器的角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 有两个级别的句柄是 ODBC 体系结构的一个项目;在大多数情况下，它与应用程序或驱动程序无关。 尽管通常没有理由这样做，但应用程序可以通过调用**SQLGetInfo**来确定驱动程序句柄。  
  
 本部分包含以下主题。  
  
-   [环境句柄](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [连接句柄](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [语句句柄](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [描述符句柄](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [状态转换](../../../odbc/reference/develop-app/state-transitions.md)
