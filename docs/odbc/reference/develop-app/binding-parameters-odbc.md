---
title: 绑定参数 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d62c0864678e116e30a0673bdf2625d70de0cedd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199604"
---
# <a name="binding-parameters-odbc"></a>绑定参数 ODBC
SQL 语句中的每个参数必须为关联，或*绑定，* 到应用程序之前执行该语句中的变量。 当应用程序将变量绑定到参数时，它描述了该驱动程序到该变量的地址、 C 数据类型等的。 它还介绍了参数本身的 SQL 数据类型、 精度和等等。 驱动程序将此信息存储在它维护适用于该语句，并使用的信息来检索该变量值时执行该语句的结构。  
  
 可绑定参数，或将其重新绑定的任意时间之前执行的语句。 如果执行语句后会重新绑定参数，直到再次执行该语句不适用于绑定。 若要将参数绑定到一个不同的变量，应用程序只需重新绑定与新的变量; 参数自动释放以前的绑定。  
  
 变量将不同的变量绑定到参数，直到通过调用所有参数之间的都绑定一直绑定到参数**SQLFreeStmt**使用 SQL_RESET_PARAMS 选项，或直到该语句被释放。 出于此原因，应用程序必须确保该变量，不会释放直到后未绑定。 有关详细信息，请参阅[Allocating 和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由于参数绑定只是存储在该语句将驱动程序维护的结构中的信息，可以按任何顺序设置它们。 它们也是独立于执行 SQL 语句。 例如，假设应用程序将绑定三个参数，然后执行以下 SQL 语句：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 如果应用程序随后立即执行 SQL 语句  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 在同一语句句柄的参数绑定**插入**使用语句，因为这些语句结构中存储的绑定。 在大多数情况下，这是好的编程做法，应避免使用。 相反，应用程序应调用**SQLFreeStmt** SQL_RESET_PARAMS 选项来取消绑定所有旧的参数，然后将新的绑定。  
  
 本部分包含以下主题。  
  
-   [绑定参数标记](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [按名称绑定参数（命名参数）](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [参数绑定偏移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [描述参数](../../../odbc/reference/develop-app/describing-parameters.md)
