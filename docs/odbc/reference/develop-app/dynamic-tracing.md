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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8420589761a1f8cb1f9cf8a3022842863fd30758
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046887"
---
# <a name="dynamic-tracing"></a>动态跟踪
在应用程序运行中的任何位置都可以启用或禁用跟踪。 这样，应用程序便可以跟踪任意数量的函数调用。  
  
 变量**ODBCSharedTraceFlag**设置为动态启用跟踪。 此变量在驱动程序管理器的所有正在运行的副本之间共享。 如果任何应用程序设置此变量，则会为当前正在运行的所有 ODBC 应用程序启用跟踪。 若要在启用动态跟踪时关闭跟踪功能，应用程序将调用**SQLSetConnectAttr** ，将 SQL_ATTR_TRACE 设置为 SQL_TRACE_OFF。 此调用只会为该应用程序关闭跟踪。 链接到 Odbc32.lib 的应用程序可以修改此变量的使用。 跟踪数据可以显示在实时窗口中，而不是显示在 ODBC 会话之后必须打开的跟踪文件中。 控件可以添加到应用程序的屏幕上，以打开或关闭跟踪。  
  
 ODBC 1.x 附带的跟踪 DLL 不*是线程安全的。* 如果启用了全局跟踪（设置了变量**ODBCSharedTraceFlag** ），并同时向跟踪文件写入了多个应用程序，则不能保证正确写入日志文件。 此条件不会返回错误。
