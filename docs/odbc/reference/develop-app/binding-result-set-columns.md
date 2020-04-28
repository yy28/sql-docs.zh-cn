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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 558ceb79d42d82477b70a028395de82cc023c170
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306358"
---
# <a name="binding-result-set-columns"></a>绑定结果集列
应用程序可以在所选的结果集中绑定任意多个或最少的列，包括根本不绑定列。 提取数据行时，驱动程序会将绑定列的数据返回到应用程序。 应用程序是否绑定结果集中的所有列取决于应用程序。 例如，生成报表的应用程序通常具有固定格式;此类应用程序将创建一个结果集，其中包含报表中使用的所有列，然后对所有这些列的数据进行绑定和检索。 显示全屏显示数据的应用程序有时允许用户确定要显示的列;此类应用程序将创建一个包含用户可能需要的所有列的结果集，但是仅绑定和检索用户选择的列的数据。  
  
 可以通过调用**SQLGetData**从未绑定的列中检索数据。 这通常被称为检索长数据，这通常超出了单个缓冲区的长度，必须在部分中进行检索。  
  
 即使提取了行后，也可以随时绑定列。 但是，新的绑定直到下一次提取行时才生效;它们不会应用于已提取的行中的数据。  
  
 在将其他变量绑定到列之前，变量保持绑定到列，直到通过调用**SQLBindCol**并将 null 指针作为该变量的地址来取消绑定所有列，直到通过使用 SQL_UNBIND 选项调用**SQLFreeStmt**来取消绑定所有列，或直到语句释放。 出于此原因，应用程序必须确保所有绑定变量在绑定后均保持有效。 有关详细信息，请参阅[分配和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由于列绑定只是与语句结构关联的信息，因此它们可以按任意顺序进行设置。 它们还独立于结果集。 例如，假设应用程序绑定以下 SQL 语句生成的结果集的列：  
  
```  
SELECT * FROM Orders  
```  
  
 如果应用程序随后执行 SQL 语句  
  
```  
SELECT * FROM Lines  
```  
  
 在同一语句句柄上，第一个结果集的列绑定仍有效，因为这些绑定是存储在语句结构中的绑定。 在大多数情况下，这是一种不太好的编程做法，应避免这样做。 相反，应用程序应调用带有 SQL_UNBIND 选项的**SQLFreeStmt** ，以取消绑定所有旧列，然后绑定新列。
