---
title: 连接属性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0fad1db10e40c71d22dd75417420c54cefa7803
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194434"
---
# <a name="connection-attributes"></a>连接属性
连接属性是连接的特征。 例如，因为事务发生在连接级别，所以事务隔离级别就是一个连接属性。 同样，登录超时值或尝试时连接超时前, 等待的秒数是连接属性。  
  
 使用设置连接属性**SQLSetConnectAttr**并使用其当前设置检索**SQLGetConnectAttr**。 如果**SQLSetConnectAttr**之前驱动程序加载时，驱动程序管理器存储在其连接结构属性并将它们作为连接过程的一部分设置驱动程序中调用。 应用程序设置任何连接属性，则不要求连接的所有属性都具有默认值，其中一些特定于驱动程序。  
  
 之前或之后的连接，或任何一个，具体取决于该属性和驱动程序，可以设置连接属性。 登录超时值 (SQL_ATTR_LOGIN_TIMEOUT) 应用于连接进程和连接前设置是才有效。 指定是否使用 ODBC 游标库 (SQL_ATTR_ODBC_CURSORS) 和网络数据包大小 (SQL_ATTR_PACKET_SIZE) 的属性之前，必须设置连接，因为 ODBC 游标库驻留之间驱动程序管理器和驱动程序和因此必须将该驱动程序之前加载。  
  
 要指定数据源是只读的还是可以设置读写 (SQL_ATTR_ACCESS_MODE) 和当前目录 (SQL_ATTR_CURRENT_CATALOG) 之前或之后连接，具体取决于驱动程序的特性。 但是，可互操作应用程序设置这些连接之前由于某些驱动程序不支持更改这些连接后。  
  
 有些连接属性之前建立连接，而其他人则不能具有默认值。 那些确实是 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT、 SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 和 SQL_ATTR_TRACEFILE。  
  
 转换连接属性 （SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION） 必须在连接后设置。  
  
 可以在任何时间设置的所有其他连接属性。 有关详细信息，请参阅[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函数说明。 (连接属性不能在环境级别上设置通过调用**SQLSetEnvAttr**。)
