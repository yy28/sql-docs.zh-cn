---
title: "绑定参数 ODBC |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 53c032a38f81b87b596e05f22137c80f5c54853c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="binding-parameters-odbc"></a>绑定参数 ODBC
SQL 语句中的每个参数必须为关联，或*绑定，*到应用程序之前执行的语句中的变量。 时应用程序将变量绑定到参数，它描述了该变量-地址、 C 数据类型和等等 — 于驱动程序。 它还描述参数本身-SQL 数据类型、 精度和等等。 该驱动程序将此信息存储在它维护适用于该语句，并使用的信息来从变量检索值时执行的语句的结构。  
  
 可以绑定或之前执行了语句随时重新绑定参数。 如果参数重新绑定之后执行某个语句，直到再次执行语句，将不适用于绑定。 将参数绑定到一个不同的变量，应用程序只需重新绑定次数与新的变量; 参数自动释放以前的绑定。  
  
 变量在一个不同的变量绑定到参数，直到所有参数都绑定通过调用一直绑定到参数**SQLFreeStmt**使用 SQL_RESET_PARAMS 选项，或释放该语句之前。 为此，应用程序必须确保该变量不会释放直到后未绑定。 有关详细信息，请参阅[Allocating 和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由于参数绑定是只是信息存储在该语句将驱动程序维护的结构，它们可以按任意顺序将此设置。 它们也是独立的 SQL 语句的执行。 例如，假设应用程序将绑定三个参数，然后执行以下 SQL 语句：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 如果应用程序然后立即执行 SQL 语句  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 在同一语句句柄的参数绑定**插入**语句使用因为这些语句结构中存储的绑定。 在大多数情况下，这是较差的编程做法，应当避免。 相反，应用程序应调用**SQLFreeStmt** SQL_RESET_PARAMS 选项来取消绑定所有旧的参数，然后将新的绑定。  
  
 本部分包含以下主题。  
  
-   [绑定参数标记](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [按名称绑定参数（命名参数）](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [参数绑定偏移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [描述参数](../../../odbc/reference/develop-app/describing-parameters.md)
