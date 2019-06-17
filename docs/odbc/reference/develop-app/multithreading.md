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
manager: craigg
ms.openlocfilehash: 1a16262d562ca2088f38cd863a6f44e537e65d40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63254211"
---
# <a name="multithreading"></a>多线程处理
多线程在操作系统上，驱动程序必须是线程安全的。 也就是说，它必须是应用程序可以在多个线程上使用相同的句柄。 这如何实现是特定于驱动程序，并可能驱动程序会将序列化任何尝试同时在两个不同的线程上使用相同的句柄。  
  
 应用程序通常使用多个线程，而不是异步处理。 应用程序创建一个单独的线程、 对其，调用 ODBC 函数，然后在主线程上继续处理。 而不是无需频繁地轮询异步函数中，使用 SQL_ATTR_ASYNC_ENABLE 语句属性时的情况一样，应用程序只需让新创建的线程完成。  
  
 接受语句句柄并在一个线程上运行的函数可以取消通过调用**SQLCancel**与同一个语句从另一个线程处理。 尽管驱动程序不应该序列化的使用**SQLCancel**以这种方式，则不能保证调用**SQLCancel**实际上将取消其他线程上运行的函数。
