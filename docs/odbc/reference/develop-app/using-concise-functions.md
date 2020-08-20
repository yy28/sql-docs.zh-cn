---
description: 使用简洁的函数
title: 使用简洁函数 |Microsoft Docs
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
ms.openlocfilehash: b0dcd16c1380c95921d5e4bb58831e2dd939ecf1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482793"
---
# <a name="using-concise-functions"></a>使用简洁的函数
某些 ODBC 函数会获得对描述符的隐式访问权限。 应用程序编写器可能会发现它们比调用 **SQLSetDescField** 或 **SQLGetDescField**更方便。 这些函数称为 *简洁* 函数，因为它们执行多个函数，包括设置或获取描述符字段。 某些简明函数允许应用程序在单个函数调用中设置或检索多个相关的描述符字段。  
  
 在未首先检索用作参数的描述符句柄的情况下，可以调用简洁函数。 这些函数适用于与调用它们的语句句柄关联的描述符字段。  
  
 简洁函数 **SQLBindCol** 和 **SQLBindParameter** 通过设置对应于参数的描述符字段来绑定列或参数。 其中每个函数执行的任务比只是设置描述符要多。 **SQLBindCol** 和 **SQLBindParameter** 提供数据列或动态参数的绑定的完整规范。 但是，应用程序可以通过调用 **SQLSetDescField** 或 **SQLSetDescRec** 来更改绑定的各个详细信息，并可以通过对这些函数进行一系列适当的调用来完全绑定列或参数。  
  
 简洁函数 **SQLColAttribute**、 **SQLDescribeCol**、 **SQLDescribeParam**、 **SQLNumParams**和 **SQLNumResultCols** 检索描述符字段中的值。  
  
 **SQLSetDescRec** 和 **SQLGetDescRec** 是一项简洁的功能，其中一次调用、设置或获取多个描述符字段，它们会影响列或参数数据的数据类型和存储。 **SQLSetDescRec** 是一种在一步中更改列或参数数据绑定的有效方法。  
  
 在某些情况下， **SQLSetStmtAttr**和**SQLGetStmtAttr**用作简洁的函数。  (参见 [描述符字段](../../../odbc/reference/develop-app/descriptor-fields.md)。 ) 
