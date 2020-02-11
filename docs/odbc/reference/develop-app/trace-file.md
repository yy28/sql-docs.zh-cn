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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67985147"
---
# <a name="trace-file"></a>跟踪文件
应用程序通过以下方式指定跟踪文件：在**TraceFile**注册表项中设置关键字，或通过使用 SQL_ATTR_TRACEFILE 连接属性调用**SQLSetConnectAttr** 。 如果启用跟踪后该文件不存在，则驱动程序管理器将创建该文件。 每个应用程序都应有自己的专用跟踪文件来避免争用。 应用程序可以使用多个跟踪文件;应用程序的安装程序可以为用户提供选择的跟踪文件。 如果动态启用跟踪，应用程序也可以显示跟踪结果，而不是记录到跟踪文件。  
  
 跟踪文件使用所有参数的数据类型和值为每个 ODBC 函数调用提供日志。 它记录所有输入函数并记录返回代码和错误状态的所有返回函数。  
  
 在 ODBC *3.x 中，* 不向跟踪 DLL 提供连接函数的参数。
