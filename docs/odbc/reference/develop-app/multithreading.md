---
title: 多线程 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c10d1b401ac780d24184c4c2337199e99973e916
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302408"
---
# <a name="multithreading"></a>多线程处理
在多线程操作系统上，驱动程序必须具有线程安全。 也就是说，应用程序必须可以在多个线程上使用相同的句柄。 如何实现这一点特定于驱动程序，并且驱动程序可能会序列化在两个不同的线程上同时使用相同的句柄的任何尝试。  
  
 应用程序通常使用多个线程而不是异步处理。 应用程序创建一个单独的线程，调用它上的 ODBC 函数，然后在主线程上继续处理。 与使用SQL_ATTR_ASYNC_ENABLE语句属性时那样，不必持续轮询异步函数，应用程序只需让新创建的线程完成即可。  
  
 可以接受语句句柄并在一个线程上运行的函数可以通过调用**SQLCancel**与另一个线程中的相同语句句柄来取消。 尽管驱动程序不应以这种方式序列化**SQLCancel**的使用，但不能保证调用**SQLCancel**实际上会取消在其他线程上运行的函数。
