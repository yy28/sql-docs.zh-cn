---
title: SQL Server 浏览示例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8dc57d738c1d5726d2208b930c5d4fadcd93b39
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47786695"
---
# <a name="sql-server-browsing-example"></a>SQL Server 浏览示例
下面的示例演示如何**SQLBrowseConnect**可能用于浏览适用于 SQL Server 驱动程序可用的连接。 首先，应用程序请求连接句柄：  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 接下来，应用程序调用**SQLBrowseConnect** ，并指定 SQL Server 驱动程序，使用返回的驱动程序的描述**SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 由于这是首次调用**SQLBrowseConnect**，驱动程序管理器来加载 SQL Server 驱动程序并调用在驱动程序**SQLBrowseConnect**与它来自的相同自变量的函数应用程序。  
  
> [!NOTE]  
>  如果您要连接到的数据源提供程序支持 Windows 身份验证，则应指定`Trusted_Connection=yes`而不是在连接字符串中的用户 ID 和密码信息。  
  
 该驱动程序确定这是首次调用**SQLBrowseConnect** ，并返回连接属性的第二个级别： 服务器、 用户名、 密码、 应用程序名称和工作站 id。 对于服务器属性，它返回有效的服务器名称的列表。 返回代码**SQLBrowseConnect**是 SQL_NEED_DATA。 下面是浏览结果字符串：  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 浏览结果字符串中的每个关键字后跟一个冒号和等号之前的一个或多个单词。 这些字是应用程序可用于生成一个对话框中的用户友好名称。 **应用程序**并**WSID**关键字前缀为星号，这意味着它们是可选的。 **服务器**， **UID**，并**PWD**关键字不能作为前缀为星号; 必须在下一步浏览请求字符串中为其提供值。 值**服务器**关键字可能返回的服务器之一**SQLBrowseConnect**或用户提供的名称。  
  
 应用程序调用**SQLBrowseConnect**同样，指定绿色的服务器，并且省略**应用**并**WSID**关键字和每个关键字后的用户友好名称：  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 驱动程序将尝试连接到绿色的服务器。 如果有任何非致命错误，如缺少关键字值对， **SQLBrowseConnect**返回 SQL_NEED_DATA 和将保持相同状态，而前错误。 应用程序可以调用**SQLGetDiagField**或**SQLGetDiagRec**来确定该错误。 如果连接成功，驱动程序返回 SQL_NEED_DATA，并返回浏览结果字符串：  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 此字符串中的属性是可选的因为该应用程序可以忽略它们。 但是，应用程序必须调用**SQLBrowseConnect**试。 如果应用程序选择省略数据库名称和语言，它指定空浏览请求字符串。 在此示例中，应用程序选择 pubs 数据库并调用**SQLBrowseConnect**最后一次，省略**语言**关键字和之前星号**数据库**关键字：  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 因为**数据库**属性是所需的驱动程序的最终的连接属性、 浏览过程已完成、 应用程序连接到数据源，并**SQLBrowseConnect**始终返回 SQL_SUCCESS。 **SQLBrowseConnect**也会返回作为浏览结果字符串的完整连接字符串：  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 返回由驱动程序的最终的连接字符串不包含每个关键字后, 用户友好名称也不会包含未指定应用程序的可选关键字。 应用程序可以使用与此字符串**SQLDriverConnect** （断开连接后） 重新连接到当前连接句柄上的数据源或连接到不同的连接句柄上的数据源。 例如：  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
