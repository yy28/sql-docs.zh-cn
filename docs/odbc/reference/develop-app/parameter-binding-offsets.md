---
title: 参数绑定偏移量 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de67b230883f3cf8a582e73ce82e8c4bd7d21ad0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282481"
---
# <a name="parameter-binding-offsets"></a>参数绑定偏移
在调用**SQLExecDirect**或**SQLExecute**时，应用程序可以指定将偏移量添加到绑定参数缓冲区地址和相应的长度/指示器缓冲区地址。 这些添加的结果决定了这些操作中使用的地址。  
  
 绑定偏移量允许应用程序更改绑定，而无需为以前绑定的参数调用**SQLBindParameter** 。 对**SQLBindParameter**的调用以重新绑定参数将更改缓冲区地址和长度/指示器指针。 另一方面，使用偏移量重新绑定，只需将偏移量添加到现有绑定参数缓冲区地址和长度/指示器缓冲区地址。 使用偏移量时，绑定是应用程序缓冲区布局方式的 "模板"，应用程序可以通过更改偏移量将此 "模板" 移到不同的内存区域。 可随时指定新偏移量，并且始终会将其添加到最初绑定的值。  
  
 为了指定绑定偏移量，应用程序将 SQL_ATTR_PARAM_BIND_OFFSET_PTR 语句特性设置为 SQLINTEGER 缓冲区的地址。 在应用程序调用使用绑定的函数之前，它将在此缓冲区中的偏移量（以字节为单位），只要参数缓冲区地址和长度/指示器缓冲区地址均不为0，并且绑定参数在 SQL 语句中。 地址与偏移量之和必须是有效地址。 （这意味着，如果其总和为有效地址，则偏移量和添加到的地址可能会无效。）  
  
> [!NOTE]  
>  ODBC 2 不支持绑定偏移量。*x*驱动程序。
