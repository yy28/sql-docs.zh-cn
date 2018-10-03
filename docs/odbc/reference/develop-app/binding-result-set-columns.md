---
title: 绑定结果集列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b92f317d72410a5dff56652dd9de1e3b2ba5c9cb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47725905"
---
# <a name="binding-result-set-columns"></a>绑定结果集列
应用程序可以作为多或较少列结果集根据他们的选择，包括所有绑定的列的绑定。 时提取的数据行，驱动程序将返回到应用程序对于绑定列的数据。 应用程序是否在结果集中绑定的所有列都取决于应用程序。 例如，通常生成报表的应用程序具有固定的格式;此类应用程序创建包含所有报表中使用的列的结果集，然后绑定并检索所有这些列的数据。 有时显示完整的数据的屏幕的应用程序允许用户决定要显示; 的列此类应用程序创建的结果集包含用户可能会想，但绑定并仅为用户选择这些列检索数据的所有列。  
  
 可以通过调用从未绑定的列检索数据**SQLGetData**。 这通常称为检索长整型数据，这通常超出了单个缓冲区的长度，必须在部件中检索。  
  
 可以在任何时候，即使已提取的行绑定列。 但是，新的绑定不会生效到下次提取行;它们不会从已提取的行应用到数据。  
  
 变量将不同的变量绑定到列，直到通过调用未绑定列的是一直绑定到列**SQLBindCol**为 null 指针作为变量的地址，直到所有列都未都绑定通过调用**SQLFreeStmt**使用 SQL_UNBIND 选项，或直到该语句被释放。 出于此原因，应用程序必须确保，只要它们所绑定的所有绑定的变量仍有效。 有关详细信息，请参阅[Allocating 和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由于列绑定只是与语句结构相关联的信息，可以按任何顺序设置它们。 它们也是独立于结果集。 例如，假设应用程序将生成的以下 SQL 语句的结果集列绑定：  
  
```  
SELECT * FROM Orders  
```  
  
 如果应用程序随后执行 SQL 语句  
  
```  
SELECT * FROM Lines  
```  
  
 在同一语句句柄，第一个结果集列绑定实际上仍的因为这些语句结构中存储的绑定。 在大多数情况下，这是好的编程做法，应避免使用。 相反，应用程序应调用**SQLFreeStmt**使用 SQL_UNBIND 选项来取消绑定所有旧的列，然后将新的绑定。
