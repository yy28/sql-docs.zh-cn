---
title: 动态跟踪 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305760"
---
# <a name="dynamic-tracing"></a>动态跟踪
在应用程序运行中的任何位置都可以启用或禁用跟踪。 这样，应用程序便可以跟踪任意数量的函数调用。  
  
 变量**ODBCSharedTraceFlag**设置为动态启用跟踪。 此变量在驱动程序管理器的所有正在运行的副本之间共享。 如果任何应用程序设置此变量，则会为当前正在运行的所有 ODBC 应用程序启用跟踪。 若要在启用动态跟踪时关闭跟踪功能，应用程序将调用**SQLSetConnectAttr** ，将 SQL_ATTR_TRACE 设置为 SQL_TRACE_OFF。 此调用只会为该应用程序关闭跟踪。 链接到 Odbc32.lib 的应用程序可以修改此变量的使用。 跟踪数据可以显示在实时窗口中，而不是显示在 ODBC 会话之后必须打开的跟踪文件中。 控件可以添加到应用程序的屏幕上，以打开或关闭跟踪。  
  
 ODBC 1.x 附带的跟踪 DLL 不*是线程安全的。* 如果启用了全局跟踪（设置了变量**ODBCSharedTraceFlag** ），并同时向跟踪文件写入了多个应用程序，则不能保证正确写入日志文件。 此条件不会返回错误。
