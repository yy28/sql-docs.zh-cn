---
title: 绑定结果集列 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306358"
---
# <a name="binding-result-set-columns"></a>绑定结果集列
应用程序可以绑定结果集的任意数量或数量少的列，包括绑定无列。 获取一行数据时，驱动程序将绑定列的数据返回给应用程序。 应用程序是否绑定结果集中的所有列取决于应用程序。 例如，生成报表的应用程序通常具有固定格式;此类应用程序创建一个结果集，其中包含报表中使用的所有列，然后绑定和检索所有这些列的数据。 显示充满数据的屏幕的应用程序有时允许用户决定要显示哪些列;此类应用程序创建一个结果集，其中包含用户可能需要的所有列，但仅为用户选择的列绑定和检索数据。  
  
 可以通过调用**SQLGetData**从未绑定列检索数据。 这通常称为检索长数据，这些数据通常超过单个缓冲区的长度，并且必须在零件中检索。  
  
 列可以随时绑定，即使在已提取行之后也是如此。 但是，新绑定直到下次提取行才会生效;它们不应用于已提取的行中的数据。  
  
 变量将保留到列，直到将另一个变量绑定到列，直到该列通过调用**SQLBindCol**与空指针作为变量的地址来取消绑定，直到所有列通过使用 SQL_UNBIND 选项调用**SQLFreeStmt**或直到语句发布而取消绑定。 因此，应用程序必须确保所有绑定变量都保持有效，只要它们被绑定。 有关详细信息，请参阅[分配和释放缓冲区](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由于列绑定只是与语句结构关联的信息，因此可以按任何顺序设置它们。 它们也独立于结果集。 例如，假设应用程序绑定由以下 SQL 语句生成的结果集的列：  
  
```  
SELECT * FROM Orders  
```  
  
 如果应用程序随后执行 SQL 语句  
  
```  
SELECT * FROM Lines  
```  
  
 在同一语句句柄上，第一个结果集的列绑定仍然有效，因为这些绑定是存储在语句结构中的绑定。 在大多数情况下，这是一种糟糕的编程实践，应避免使用。 相反，应用程序应使用SQL_UNBIND选项调用**SQLFreeStmt，** 以取消绑定所有旧列，然后绑定新列。
