---
title: 参数绑定偏移量 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282481"
---
# <a name="parameter-binding-offsets"></a>参数绑定偏移
应用程序可以指定在调用**SQLExecDirect**或**SQLExecute**时将偏移量添加到绑定参数缓冲区地址和相应的长度/指示器缓冲区地址。 这些添加的结果确定这些操作中使用的地址。  
  
 绑定偏移允许应用程序更改绑定，而无需为以前绑定的参数调用**SQLBind 参数**。 调用**SQLBind参数**以重新绑定参数会更改缓冲区地址和长度/指示器指针。 另一方面，使用偏移重新绑定只需向现有绑定参数缓冲区地址和长度/指示器缓冲区地址添加偏移。 使用偏移时，绑定是应用程序缓冲区布局方式的"模板"，应用程序可以通过更改偏移量将此"模板"移动到不同的内存区域。 可以随时指定新的偏移量，并且始终添加到最初绑定的值。  
  
 要指定绑定偏移量，应用程序将SQL_ATTR_PARAM_BIND_OFFSET_PTR语句属性设置到 SQLINTEGER 缓冲区的地址。 在应用程序调用使用绑定的函数之前，只要参数缓冲区地址和长度/指示器缓冲区地址都不是 0，并且绑定参数在 SQL 语句中，它将在此缓冲区中放置一个偏移以字节为单位。 地址和偏移量的总和必须为有效地址。 （这意味着偏移量和添加到偏移的地址都无效，只要其总和是有效的地址。  
  
> [!NOTE]  
>  ODBC 2 不支持绑定偏移。*x*驱动程序。
