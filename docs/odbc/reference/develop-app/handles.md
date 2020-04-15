---
title: 手柄 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300207"
---
# <a name="handles"></a>控点
句柄是不透明的 32 位值，用于标识特定项;在 ODBC 中，此项目可以是环境、连接、语句或描述符。 当应用程序调用**SQLAllocHandle**时，驱动程序管理器或驱动程序将创建指定类型的新项，并将其句柄返回到应用程序。 应用程序稍后使用句柄在调用 ODBC 函数时标识该项。 驱动程序管理器和驱动程序使用句柄查找有关该项目的信息。  
  
 例如，以下代码使用两个语句句柄 *（hstmtOrder 和* *hstmtLine）* 来标识要创建销售订单和销售订单行号的结果集的语句。 它稍后使用这些句柄来标识要从哪个结果集获取数据。  
  
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
  
 句柄仅对创建句柄的 ODBC 组件有意义;也就是说，只有驱动程序管理器可以解释驱动程序管理器句柄，只有驱动程序可以解释其自己的句柄。  
  
 例如，假设前面的示例中的驱动程序分配一个结构来存储有关语句的信息，并将指向此结构的指针作为语句句柄返回。 当应用程序调用**SQLPrepare**时，它将传递一个 SQL 语句和用于销售订单行号的语句的句柄。 驱动程序将 SQL 语句发送到数据源，数据源会准备它并返回访问计划标识符。 驱动程序使用句柄查找要存储此标识符的结构。  
  
 稍后，当应用程序调用**SQLExecute**生成特定销售订单的结果行号集时，它将传递相同的句柄。 驱动程序使用句柄从结构中检索访问计划标识符。 它将标识符发送到数据源，告诉它要执行哪个计划。  
  
 ODBC 有两个级别的句柄：驱动程序管理器句柄和驱动程序句柄。 应用程序在调用 ODBC 函数时使用驱动程序管理器句柄，因为它在驱动程序管理器中调用这些函数。 驱动程序管理器使用此句柄查找相应的驱动程序句柄，并在在驱动程序中调用函数时使用驱动程序句柄。 有关如何使用驱动程序和驱动程序管理器句柄的示例，请参阅[驱动程序管理器在连接过程中的角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 有两个级别的句柄是 ODBC 体系结构的工件;在大多数情况下，它与应用程序或驱动程序无关。 尽管通常没有理由这样做，但应用程序可以通过调用**SQLGetInfo**来确定驱动程序句柄。  
  
 本部分包含以下主题。  
  
-   [环境句柄](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [连接句柄](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [语句句柄](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [描述符句柄](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [状态转换](../../../odbc/reference/develop-app/state-transitions.md)
