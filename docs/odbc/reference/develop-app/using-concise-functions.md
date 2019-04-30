---
title: 使用简洁的函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d70d3ca60a046a355549260406edba261f805e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312482"
---
# <a name="using-concise-functions"></a>使用简洁的函数
某些 ODBC 函数获取描述符的隐式访问权限。 应用程序编写器可能会发现它们相对于调用更方便**SQLSetDescField**或**SQLGetDescField**。 调用这些函数*简洁*函数由于它们执行的许多功能，包括设置或获取描述符字段。 一些简洁的函数允许应用程序设置或检索单个函数调用中的多个相关的描述符字段。  
  
 简洁的函数可以调用而无需第一个检索使用作为参数的描述符句柄。 这些函数使用与语句句柄关联调用的描述符字段。  
  
 简洁的函数**SQLBindCol**并**SQLBindParameter**通过将相对应的描述符字段设置为其参数绑定的列或参数。 每个函数执行比只需设置描述符的更多任务。 **SQLBindCol**并**SQLBindParameter**提供的数据列或动态参数绑定的完整规范。 应用程序可以但是，通过调用更改绑定的详细信息**SQLSetDescField**或**SQLSetDescRec** ，并且可用于一系列到合适的调用，从而完全绑定的列或参数这些函数。  
  
 简洁的函数**SQLColAttribute**， **SQLDescribeCol**， **SQLDescribeParam**， **SQLNumParams**，和**SQLNumResultCols**检索描述符字段中的值。  
  
 **SQLSetDescRec**并**SQLGetDescRec**是简洁的函数，使用一次调用设置或获取影响的数据类型和列或参数的数据的存储的多个描述符字段。 **SQLSetDescRec**是一种有效的方法来更改在一个步骤中的列或参数的数据绑定。  
  
 **SQLSetStmtAttr**并**SQLGetStmtAttr**充当简洁的函数，在某些情况下。 (请参阅[描述符字段](../../../odbc/reference/develop-app/descriptor-fields.md)。)
