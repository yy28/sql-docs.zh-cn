---
title: 使用简明功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63313e3dfaec8dbcd91f3bb084bbaab46da40c6e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306778"
---
# <a name="using-concise-functions"></a>使用简洁的函数
某些 ODBC 函数获得对描述符的隐式访问。 应用程序编写者可能会发现它们比调用**SQLSetDescField**或**SQLGetDescField**更方便。 这些函数称为*简洁*函数，因为它们执行许多函数，包括设置或获取描述符字段。 某些简洁的函数允许应用程序在单个函数调用中设置或检索多个相关的描述符字段。  
  
 可以调用简洁函数，而无需首先检索描述符句柄以用作参数。 这些函数与调用它们的语句句柄关联的描述符字段一起工作。  
  
 简洁函数**SQLBindCol**和**SQLBindParameter**通过设置与其参数对应的描述符字段来绑定列或参数。 与简单地设置描述符相比，每个函数执行的任务都更多。 **SQLBindCol**和**SQLBind参数**提供了数据列或动态参数绑定的完整规范。 但是，应用程序可以通过调用**SQLSetDescField**或**SQLSetDescRec**来更改绑定的单个详细信息，并且可以通过对这些函数进行一系列适当的调用来完全绑定列或参数。  
  
 简洁函数**SQLColAttribute**SQLColAttribute、SQLDescribeCol、SQLDescribeParam、SQLNumParams 和**SQLNumResultCols**检索描述符字段中的值。 **SQLDescribeCol** **SQLDescribeParam** **SQLNumParams**  
  
 **SQLSetDescRec**和**SQLGetDescRec**是简洁的函数，通过一次调用，设置或获取多个影响列或参数数据的数据类型和存储的描述符字段。 **SQLSetDescRec**是一步更改列或参数数据的绑定的有效方法。  
  
 **在某些情况下，SQLSetStmtAttr**和**SQLGetStmtAttr**充当简洁的功能。 （请参阅[描述符字段](../../../odbc/reference/develop-app/descriptor-fields.md)。
