---
title: "连接属性 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8674cb60df26d15539beef1f46a74233bf838625
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="connection-attributes"></a>连接属性
连接属性是连接的特性。 例如，因为事务发生在连接级别，所以事务隔离级别就是一个连接属性。 同样，登录超时值或尝试时连接超时前, 等待的秒数是连接属性。  
  
 连接属性设置与**SQLSetConnectAttr**和使用它们的当前设置检索**SQLGetConnectAttr**。 如果**SQLSetConnectAttr**驱动程序已加载，驱动程序管理器将这些属性存储在其连接结构，并将它们驱动程序中设置连接过程的一部分之前调用。 应用程序设置任何连接属性，则不要求所有连接属性都具有默认值，其中有一些特定于驱动程序。  
  
 之前或之后连接，或任何一个，具体取决于属性和驱动程序，可以设置连接属性。 登录超时值 (SQL_ATTR_LOGIN_TIMEOUT) 适用于连接过程和有效才设置连接之前。 指定是否使用 ODBC 游标库 (SQL_ATTR_ODBC_CURSORS) 和网络数据包大小 (SQL_ATTR_PACKET_SIZE) 的属性必须设置连接之前，，因为 ODBC 游标库所在之间驱动程序管理器和驱动程序和因此必须加载驱动程序之前。  
  
 要指定数据源是只读的还是之前或之后连接，具体取决于该驱动程序，可以设置读写 (SQL_ATTR_ACCESS_MODE) 和当前目录 (SQL_ATTR_CURRENT_CATALOG) 的属性。 但是，可互操作的应用程序设置它们在连接之前由于某些驱动程序不支持更改这些连接后。  
  
 某些连接属性之前建立连接，而其他则不能具有默认值。 这样做的那些是 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT、 SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 和 SQL_ATTR_TRACEFILE。  
  
 连接后，必须设置翻译连接属性 （SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION）。  
  
 在任何时候，可以设置所有其他连接属性。 有关详细信息，请参阅[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函数说明。 (通过调用，不能在环境级别上设置连接属性**SQLSetEnvAttr**。)
