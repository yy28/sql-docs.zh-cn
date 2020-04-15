---
title: 绑定参数 ODBC |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306378"
---
# <a name="binding-parameters-odbc"></a>绑定参数 ODBC
在执行语句之前，SQL 语句中的每个参数都必须关联或*绑定*到应用程序中的变量。 当应用程序将变量绑定到参数时，它将该变量 （ 地址、 C 数据类型等 ） 描述到驱动程序。 它还描述了参数本身 - SQL 数据类型、精度等。 驱动程序将此信息存储在它为该语句维护的结构中，并使用该信息在执行语句时从变量中检索值。  
  
 在执行语句之前，可以随时绑定或反弹参数。 如果参数在执行语句后反弹，则绑定在语句再次执行之前不适用。 要将参数绑定到其他变量，应用程序只需将参数与新变量重新绑定即可;以前的绑定将自动释放。  
  
 变量将保留到参数，直到将不同的变量绑定到参数，直到所有参数通过使用 SQL_RESET_PARAMS 选项调用**SQLFreeStmt**或直到语句发布来取消绑定。 因此，应用程序必须确保在变量未绑定之前不会释放它们。 有关详细信息，请参阅[分配和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由于参数绑定只是存储在语句的驱动程序维护的结构中的信息，因此可以按任何顺序设置它们。 它们也独立于执行的 SQL 语句。 例如，假设应用程序绑定三个参数，然后执行以下 SQL 语句：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 如果应用程序然后立即执行 SQL 语句  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 在同一语句句柄上，使用**INSERT**语句的参数绑定，因为这些绑定存储在语句结构中。 在大多数情况下，这是一种糟糕的编程实践，应避免使用。 相反，应用程序应使用SQL_RESET_PARAMS选项调用**SQLFreeStmt，** 以取消绑定所有旧参数，然后绑定新参数。  
  
 本部分包含以下主题。  
  
-   [绑定参数标记](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [按名称绑定参数（命名参数）](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [参数绑定偏移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [描述参数](../../../odbc/reference/develop-app/describing-parameters.md)
