---
title: 跟踪文件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c94c3718c116b37eb198264887dfb4a319bd1dc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985147"
---
# <a name="trace-file"></a>跟踪文件
应用程序指定的跟踪文件可以通过设置**TraceFile**关键字在 Odbc.ini 注册表项或通过调用**SQLSetConnectAttr** SQL_ATTR_TRACEFILE 连接属性。 如果启用跟踪时，该文件不存在，驱动程序管理器将创建该文件。 每个应用程序应具有其自己专用的跟踪文件以避免出现争用。 应用程序可以使用多个跟踪文件;应用程序的安装程序可以向用户提供选择的跟踪文件。 如果动态启用跟踪，应用程序还可以显示跟踪结果，而不是日志记录到跟踪文件。  
  
 跟踪文件提供的数据类型与每个 ODBC 函数调用的日志和所有参数的值。 它将记录所有输入的函数，并使用返回代码和错误状态记录返回的所有函数。  
  
 在 ODBC *3.x*，连接函数的参数未提供跟踪 DLL。
