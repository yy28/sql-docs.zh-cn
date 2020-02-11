---
title: 多线程 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086354"
---
# <a name="multithreading"></a>多线程处理
在多线程操作系统中，驱动程序必须是线程安全的。 也就是说，应用程序必须能够在多个线程上使用相同的句柄。 如何实现此目的是特定于驱动程序的，而且驱动程序可能会序列化尝试同时在两个不同的线程上使用相同的句柄。  
  
 应用程序通常使用多个线程，而不是异步处理。 应用程序创建一个单独的线程，对其调用 ODBC 函数，然后在主线程上继续处理。 由于使用的是 SQL_ATTR_ASYNC_ENABLE 语句特性，因此，应用程序只需让新创建的线程完成，就不必持续轮询异步函数。  
  
 对于接受语句句柄并在一个线程上运行的函数，可以通过从另一个线程的相同语句句柄调用**SQLCancel**来取消。 尽管驱动程序不应以这种方式序列化使用**SQLCancel** ，但并不保证调用**SQLCancel**实际上会取消在另一个线程上运行的函数。
