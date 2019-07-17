---
title: 多线程处理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1eaa07ce22436bc8bfae215c0431480081ee0f06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086354"
---
# <a name="multithreading"></a>多线程处理
多线程在操作系统上，驱动程序必须是线程安全的。 也就是说，它必须是应用程序可以在多个线程上使用相同的句柄。 这如何实现是特定于驱动程序，并可能驱动程序会将序列化任何尝试同时在两个不同的线程上使用相同的句柄。  
  
 应用程序通常使用多个线程，而不是异步处理。 应用程序创建一个单独的线程、 对其，调用 ODBC 函数，然后在主线程上继续处理。 而不是无需频繁地轮询异步函数中，使用 SQL_ATTR_ASYNC_ENABLE 语句属性时的情况一样，应用程序只需让新创建的线程完成。  
  
 接受语句句柄并在一个线程上运行的函数可以取消通过调用**SQLCancel**与同一个语句从另一个线程处理。 尽管驱动程序不应该序列化的使用**SQLCancel**以这种方式，则不能保证调用**SQLCancel**实际上将取消其他线程上运行的函数。
