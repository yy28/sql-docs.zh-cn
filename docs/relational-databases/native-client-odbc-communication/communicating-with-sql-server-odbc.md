---
title: 与 SQL Server (ODBC) 通信 |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 12bc416141e877170d9dfb06c9504a913ffb4c4e
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698948"
---
# <a name="communicating-with-sql-server-odbc"></a>与 SQL Server 通信 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 应用程序的实例与进行通信的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，它必须分配环境和连接处理并连接到数据源。 在建立连接后，应用程序可以向服务器发送查询并处理任意结果集。 应用程序使用完数据源后，它断开与数据源的连接并释放连接句柄。 应用程序释放所有连接句柄后，将释放环境句柄。  
  
 一个应用程序可以与任意数目的数据源连接。 该应用程序可以使用多个驱动程序和多个数据源的组合、同一驱动程序和多个数据源的组合，甚至可以使用同一驱动程序和指向同一数据源的多个连接。  
  
 你可以下载[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 示例从[SQL Server 下载](http://go.microsoft.com/fwlink/?LinkId=62796)MSDN 上的页。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [分配环境句柄](../../relational-databases/native-client-odbc-communication/allocating-an-environment-handle.md)  
  
-   [分配连接句柄](../../relational-databases/native-client-odbc-communication/allocating-a-connection-handle.md)  
  
-   [SQL Server Native Client ODBC 数据源](../../relational-databases/native-client-odbc-communication/sql-server-native-client-odbc-data-sources.md)  
  
-   [连接到数据源&#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md)  
  
-   [与数据源断开连接](../../relational-databases/native-client-odbc-communication/disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)  
  
  
