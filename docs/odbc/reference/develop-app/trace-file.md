---
title: 跟踪文件 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddd0ee24649592cf4a1a296a51404334145a3bab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298054"
---
# <a name="trace-file"></a>跟踪文件
应用程序通过在 Odbc.ini 注册表条目中设置**TraceFile**关键字或使用SQL_ATTR_TRACEFILE连接属性调用**SQLSetConnectAttr**来指定跟踪文件。 如果启用跟踪时文件不存在，驱动程序管理器将创建该文件。 每个应用程序都应有自己的专用跟踪文件，以避免争用。 应用程序可以使用多个跟踪文件;但是，应用程序可以使用多个跟踪文件。应用程序的安装程序可以为用户提供跟踪文件的选择。 如果动态启用了跟踪，则应用程序还可以显示跟踪结果，而不是登录到跟踪文件。  
  
 跟踪文件提供每个 ODBC 函数调用的日志，包含所有参数的数据类型和值。 它记录所有输入函数，并记录所有返回的函数，并带有返回代码和错误状态。  
  
 在 ODBC *3.x*中，连接函数的参数不提供给跟踪 DLL。
