---
title: "SQL Server 浏览示例 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a7076a1a1fad871c03c55ef87e87591d45acb3a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sql-server-browsing-example"></a>SQL 服务器浏览示例
下面的示例演示如何**SQLBrowseConnect**可能用于浏览 SQL Server 提供了驱动程序的连接。 第一次，应用程序请求连接句柄：  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 接下来，应用程序调用**SQLBrowseConnect** ，并指定 SQL Server 驱动程序，使用通过返回的驱动程序说明**SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 因为这是首次调用**SQLBrowseConnect**，驱动程序管理器来加载 SQL Server 驱动程序并调用驱动程序的**SQLBrowseConnect**与从其接收的相同自变量的函数应用程序。  
  
> [!NOTE]  
>  如果你要连接到的数据源提供程序支持 Windows 身份验证，你应指定`Trusted_Connection=yes`而不是连接字符串中的用户 ID 和密码信息。  
  
 该驱动程序确定这是首次调用**SQLBrowseConnect**并返回连接属性的第二个级别： 服务器、 用户名称、 密码、 应用程序名称和工作站 id。 对于服务器属性中，它返回有效的服务器名称的列表。 返回代码**SQLBrowseConnect**是 SQL_NEED_DATA。 下面是浏览结果字符串：  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 浏览结果字符串中的每个关键字后跟一个冒号和等号之前的一个或多个单词。 这些单词是应用程序可用于生成对话框中的用户友好名称。 **应用**和**WSID**关键字的前缀为一个星号，这意味着为可选。 **服务器**， **UID**，和**PWD**关键字不带前缀，用星号; 必须在下一步浏览请求字符串中为它们提供值。 值**服务器**关键字可能返回的服务器之一**SQLBrowseConnect**或用户提供的名称。  
  
 应用程序调用**SQLBrowseConnect**同样，指定绿色服务器以及省略**应用**和**WSID**关键字和每个关键字之后的用户友好名称：  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 该驱动程序尝试连接到绿色的服务器。 如果有任何非致命错误，如缺少的关键字 / 值对， **SQLBrowseConnect**返回 SQL_NEED_DATA 并保留在相同的状态，因为其在发生错误前。 应用程序可以调用**SQLGetDiagField**或**SQLGetDiagRec**以确定该错误。 如果连接成功，驱动程序返回 SQL_NEED_DATA，并返回浏览结果字符串：  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 此字符串中的属性是可选的因为应用程序可以忽略它们。 但是，应用程序必须调用**SQLBrowseConnect**试。 如果应用程序选择省略数据库名称和语言，它指定一个空浏览请求字符串。 在此示例中，应用程序选择的 pubs 数据库和调用**SQLBrowseConnect**最后一次，省略**语言**关键字和之前星号**数据库**关键字：  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 因为**数据库**属性是由驱动程序所需的最终的连接属性、 浏览过程已完成、 应用程序连接到数据源和**SQLBrowseConnect**返回 SQL_SUCCESS。 **SQLBrowseConnect**也会返回作为浏览结果字符串的完整连接字符串：  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 返回由驱动程序的最后一个连接字符串不包含每个关键字后, 的用户友好名称，也不包含未指定的应用程序的可选关键字。 应用程序可以使用与此字符串**SQLDriverConnect** （后，从断开连接） 重新连接到当前连接句柄上的数据源，或连接到不同的连接句柄上的数据源。 例如：  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
