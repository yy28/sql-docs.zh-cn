---
title: 动态跟踪 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], dynamic
- dynamic tracing [ODBC]
ms.assetid: ebe58a83-a7b0-4747-86c8-2af2940471ef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8cbd2dbae4f4b437f45845ce2791f4a9b0aa8c8b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305760"
---
# <a name="dynamic-tracing"></a>动态跟踪
可以在应用程序运行的任何点启用或禁用跟踪。 这允许应用程序跟踪任意数量的函数调用。  
  
 变量**ODBCSharedTraceFlag**设置为动态启用跟踪。 此变量在驱动程序管理器的所有正在运行的副本之间共享。 如果任何应用程序设置此变量，则为当前运行的所有 ODBC 应用程序启用跟踪。 要在启用动态跟踪时关闭跟踪，应用程序将调用**SQLSetConnectAttr**以将SQL_ATTR_TRACE设置为SQL_TRACE_OFF。 此调用将仅关闭该应用程序的跟踪。 与 Odbc32.lib 链接的应用程序可以修改此变量的使用。 跟踪数据可以显示在实时窗口中，而不是跟踪文件，必须在 ODBC 会话后打开。 可以将控件添加到应用程序的屏幕以打开或关闭跟踪。  
  
 ODBC 3 *.x*附带的跟踪 DLL 不具有线程安全。 如果启用了全局跟踪（设置了变量**ODBCSharedTraceFlag），** 并且多个应用程序同时写入跟踪文件，则不能保证日志文件的写入正确。 此条件不会返回错误。
