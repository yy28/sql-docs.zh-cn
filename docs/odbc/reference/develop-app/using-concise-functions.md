---
title: "使用简洁函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5559250002983b942601311b04e1f4ae2eac49a2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-concise-functions"></a>使用简洁的函数
某些 ODBC 函数向描述符隐式访问。 应用程序编写器可能会发现它们比调用更方便**SQLSetDescField**或**SQLGetDescField**。 调用这些函数的*简洁*函数因为它们执行的许多功能，包括设置或获取描述符字段。 某些简洁函数允许应用程序设置或检索单个函数调用中的多个相关的描述符字段。  
  
 可以在未第一个检索作为自变量的使用的描述符句柄的情况下调用简洁的函数。 这些函数使用在调用的描述符字段与语句句柄关联。  
  
 简洁函数**SQLBindCol**和**SQLBindParameter**通过将对应的描述符字段设置为其自变量绑定的列或参数。 其中每个函数执行比只设置描述符的多个任务。 **SQLBindCol**和**SQLBindParameter**提供的绑定中的数据列或动态参数的完整规范。 应用程序但是，可以通过调用更改的绑定的详细信息**SQLSetDescField**或**SQLSetDescRec** ，并且可用于通过进行一系列到适合调用完全绑定的列或参数这些函数。  
  
 简洁函数**SQLColAttribute**， **SQLDescribeCol**， **SQLDescribeParam**， **SQLNumParams**，和**SQLNumResultCols**检索描述符字段中的值。  
  
 **SQLSetDescRec**和**SQLGetDescRec**是简洁的函数，使用一次调用，设置或获取影响的数据类型和列或参数的数据的存储的多个描述符字段。 **SQLSetDescRec**是一种有效的方法来更改的一个步骤中的列或参数的数据绑定。  
  
 **SQLSetStmtAttr**和**SQLGetStmtAttr**用作简洁函数在某些情况下。 (请参阅[描述符字段](../../../odbc/reference/develop-app/descriptor-fields.md)。)
