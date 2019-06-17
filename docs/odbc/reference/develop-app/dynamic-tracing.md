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
manager: craigg
ms.openlocfilehash: 63dbfda01d96cad53e5830e598b5812ed79d8f04
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468774"
---
# <a name="dynamic-tracing"></a>动态跟踪
可以启用或禁用运行的应用程序中的任何位置跟踪。 这允许应用程序跟踪任意数量的函数调用。  
  
 在变量**ODBCSharedTraceFlag**设置以启用动态跟踪。 此变量是在所有运行副本的驱动程序管理器之间共享。 如果任何应用程序设置此变量，为所有当前正在运行的 ODBC 应用程序启用跟踪。 若要启用关闭时启用了动态跟踪的跟踪，应用程序调用**SQLSetConnectAttr** SQL_ATTR_TRACE 设 SQL_TRACE_OFF。 此调用将关闭该应用程序关闭跟踪。 使用 odbc32.lib 进行链接的应用程序可以修改此变量的用途。 可以在实时窗口中，而不是 ODBC 会话后，必须打开跟踪文件显示跟踪数据。 控件可以添加到应用程序的屏幕，若要启用将在打开或关闭跟踪。  
  
 跟踪 DLL 随 ODBC 3 *.x*不是线程安全的。 不保证日志文件编写正确，如果启用全局跟踪 (变量**ODBCSharedTraceFlag**设置) 和多个应用程序在同一时间将写入到跟踪文件。 这种情况不会返回错误。
