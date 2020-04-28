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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e314bb9e3a1a979976a450e2a45a286ec54dfe7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306378"
---
# <a name="binding-parameters-odbc"></a>绑定参数 ODBC
在执行语句前，必须将 SQL 语句中的每个参数关联或*绑定*到应用程序中的变量。 当应用程序将变量绑定到参数时，它会对驱动程序描述变量地址、C 数据类型等。 还介绍了参数本身-SQL 数据类型、精度等。 驱动程序将此信息存储在它为该语句维护的结构中，并在执行语句时使用该信息检索变量中的值。  
  
 在执行语句之前，可以随时绑定或重新绑定参数。 如果在执行语句后重新绑定参数，则在再次执行该语句之前，将不会应用绑定。 若要将参数绑定到不同的变量，应用程序只需使用新变量重新绑定参数;上一个绑定会自动释放。  
  
 在将其他变量绑定到参数之前，变量保持绑定到参数，直到通过使用 SQL_RESET_PARAMS 选项调用**SQLFreeStmt**来解除所有参数的绑定，或直到语句释放。 出于此原因，应用程序必须确保在变量未绑定之前不会将其释放。 有关详细信息，请参阅[分配和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由于参数绑定只是存储在由语句的驱动程序所维护的结构中的信息，因此可按任意顺序进行设置。 它们还独立于所执行的 SQL 语句。 例如，假设应用程序绑定三个参数，然后执行以下 SQL 语句：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 如果应用程序随后立即执行 SQL 语句  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 在同一语句句柄上，使用**INSERT**语句的参数绑定，因为这些是存储在语句结构中的绑定。 在大多数情况下，这是一种不太好的编程做法，应避免这样做。 相反，应用程序应调用带有 SQL_RESET_PARAMS 选项的**SQLFreeStmt** ，以取消所有旧参数的绑定，然后绑定新参数。  
  
 本部分包含以下主题。  
  
-   [绑定参数标记](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [按名称绑定参数（命名参数）](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [参数绑定偏移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [描述参数](../../../odbc/reference/develop-app/describing-parameters.md)
