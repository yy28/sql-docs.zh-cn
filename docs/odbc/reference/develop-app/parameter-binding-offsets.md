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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d0dbddc71b0d647246d10dad16ad72d533df16de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023340"
---
# <a name="parameter-binding-offsets"></a>参数绑定偏移
应用程序可以指定偏移量添加绑定参数缓冲区地址和相应的长度/指示器缓冲区地址何时**SQLExecDirect**或**SQLExecute**调用。 这些新增功能的结果确定这些操作中使用的地址。  
  
 绑定的偏移量允许应用程序更改而无需调用绑定**SQLBindParameter**以前绑定参数。 调用**SQLBindParameter**重新绑定参数更改的缓冲区地址和长度/指示器指针。 重新绑定带有偏移量，另一方面，只需将偏移量添加到现有的绑定的参数缓冲区地址和长度/指示器缓冲区地址。 当使用偏移量时，绑定是一个"模板"的应用程序缓冲区的布局方式和应用程序可此"模板"通过移动到不同区域的内存更改偏移量。 新的偏移量可以指定在任何时间，并且始终添加到最初绑定值。  
  
 若要指定绑定偏移量，该应用程序设置为 SQLINTEGER 缓冲区的地址的 SQL_ATTR_PARAM_BIND_OFFSET_PTR 语句属性。 应用程序调用一个函数，使用这些绑定之前，它将偏移量中此缓冲区中的字节，只要参数缓冲区地址和长度/指示器缓冲区地址都不为 0，且绑定的参数为 SQL 语句中。 地址和偏移量的总和必须为有效的地址。 （这意味着，一个或两个偏移量和偏移量添加到的地址可以是无效的其总和为有效的地址。）  
  
> [!NOTE]  
>  绑定的偏移量不受 ODBC 2。*x*驱动程序。
