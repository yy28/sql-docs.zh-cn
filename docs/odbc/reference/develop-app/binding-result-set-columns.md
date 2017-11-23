---
title: "设置列的绑定结果 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cafac55eeca169ff83521e945f0f5e76b31f19c8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="binding-result-set-columns"></a>设置列的绑定结果
应用程序可以为多或尽可能少的结果集根据他们的选择，包括在所有绑定没有列的列将绑定。 时提取数据行，该驱动程序将返回到应用程序对于绑定列的数据。 应用程序是否在结果集中绑定的所有列都取决于应用程序。 例如，应用程序通常生成报表具有固定的格式;此类应用程序创建一个包含所有报表中使用的列的结果集，然后将绑定和检索所有这些列的数据。 有时显示屏幕完整的数据的应用程序允许用户决定哪些列显示;此类应用程序创建的结果集包含用户可能想，但将绑定和检索由用户选择这些列的数据的所有列。  
  
 可以通过调用从未绑定列检索数据**SQLGetData**。 这通常称为检索长整型数据，也不能通常超过单个缓冲区的长度必须在部件中检索到。  
  
 可以在任何时候，即使在提取行绑定列。 但是，新的绑定不会生效到下次提取行;它们不应用数据从已提取的行。  
  
 一个不同的变量绑定到列中，直到列绑定通过调用一直绑定到列变量**SQLBindCol**替换为 null 指针为变量的地址，直到所有列都未都绑定通过调用**SQLFreeStmt**使用 SQL_UNBIND 选项，或释放该语句之前。 为此，应用程序必须确保所有绑定的变量保持有效，只要它们被绑定。 有关详细信息，请参阅[Allocating 和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由于列绑定是只是与语句结构相关联的信息，它们可以按任意顺序将此设置。 它们也是独立于结果集。 例如，假设应用程序将生成的以下 SQL 语句的结果集的列绑定：  
  
```  
SELECT * FROM Orders  
```  
  
 然后，应用程序执行的 SQL 语句  
  
```  
SELECT * FROM Lines  
```  
  
 在相同的语句句柄，第一个结果集的列绑定仍实际上的因为这些语句结构中存储的绑定。 在大多数情况下，这是较差的编程做法，应当避免。 相反，应用程序应调用**SQLFreeStmt** SQL_UNBIND 选项来取消绑定所有旧的列，然后将新的绑定。
