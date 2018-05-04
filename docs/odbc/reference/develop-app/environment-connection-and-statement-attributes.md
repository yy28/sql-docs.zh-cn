---
title: 环境、 连接和语句属性 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe71bb625852f6b404c6e27ff9cdf406df4ea0b3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="environment-connection-and-statement-attributes"></a>环境、 连接和语句属性
ODBC 定义大量的与环境、 连接或语句相关联的属性。  
  
 环境属性会影响整个环境，例如是否启用连接池。 环境属性设置与**SQLSetEnvAttr**和与检索到**SQLGetEnvAttr**。  
  
 连接属性会影响每个连接单独，例如如何驱动程序时尝试连接到数据源在超时前应等待的长时间。连接属性设置与**SQLSetConnectAttr**和与检索到**SQLGetConnectAttr**。 有关连接属性的详细信息，请参阅[连接属性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 语句特性影响每个语句单独，如是否应以异步方式执行某个语句。 与设置语句属性**SQLSetStmtAttr**和与检索到**SQLGetStmtAttr**。 几个语句属性是只读属性，且无法进行设置。 例如，用于检索中光标的当前行数的 SQL_ATTR_ROW_NUMBER 语句属性是只读的。 有关语句特性的详细信息，请参阅[语句特性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 除了属性定义的 ODBC 驱动程序可以定义其自己的连接和语句属性。 驱动程序定义的特性必须注册与打开组，以确保两个的驱动程序供应商现在将相同的整数值分配给不同的、 专用属性。 有关详细信息，请参阅[特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 属性的完整列表，请参阅[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)， [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，和[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。 这些设置会影响该 ODBC 函数的说明中也描述了大多数属性。
