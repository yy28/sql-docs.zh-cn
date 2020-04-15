---
title: 连接属性 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c295ce88eedf1d4cddc4173f5dea39c44b01f83d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299038"
---
# <a name="connection-attributes"></a>连接属性
连接属性是连接的特征。 例如，因为事务发生在连接级别，所以事务隔离级别就是一个连接属性。 同样，登录超时，或尝试连接时等待的秒数，在超时之前，是一个连接属性。  
  
 连接属性是使用**SQLSetConnectAttr**设置的，并且其当前设置使用**SQLGetConnectAttr**检索。 如果在加载驱动程序之前调用**SQLSetConnectAttr，** 驱动程序管理器将属性存储在其连接结构中，并将其设置为驱动程序中的连接过程的一部分。 没有要求应用程序设置任何连接属性;所有连接属性都有默认值，其中一些是特定于驱动程序的。  
  
 连接属性可以在连接之前或之后设置，也可以设置，具体取决于属性和驱动程序。 登录超时（SQL_ATTR_LOGIN_TIMEOUT）适用于连接过程，仅在连接前设置时才有效。 在连接之前，必须设置指定是否使用 ODBC 游标库 （SQL_ATTR_ODBC_CURSORS） 和网络数据包大小 （SQL_ATTR_PACKET_SIZE）的属性，因为 ODBC 游标库位于驱动程序管理器和驱动程序之间，因此必须在驱动程序之前加载。  
  
 指定数据源是只读还是读写 （SQL_ATTR_ACCESS_MODE） 和当前目录 （SQL_ATTR_CURRENT_CATALOG） 的属性可以在连接之前或之后设置，具体取决于驱动程序。 但是，可互操作的应用程序在连接前设置它们，因为某些驱动程序不支持在连接后更改它们。  
  
 某些连接属性在建立连接之前具有默认值，而其他连接属性则没有默认值。 那些做是SQL_ATTR_ACCESS_MODE，SQL_ATTR_AUTOCOMMIT，SQL_ATTR_LOGIN_TIMEOUT，SQL_ATTR_ODBC_CURSORS，SQL_ATTR_TRACE和SQL_ATTR_TRACEFILE。  
  
 连接后必须设置转换连接属性（SQL_ATTR_TRANSLATE_DLL和SQL_ATTR_TRANSLATE_OPTION）。  
  
 可以随时设置所有其他连接属性。 有关详细信息，请参阅[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函数说明。 （无法通过调用**SQLSetEnvAttr**在环境级别设置连接属性。
