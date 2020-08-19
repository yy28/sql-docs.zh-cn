---
description: SQL Server 浏览示例
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14016832989c6fcba1dc39bc64434e72b049c18a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424559"
---
# <a name="sql-server-browsing-example"></a>SQL Server 浏览示例
下面的示例演示如何使用 **SQLBrowseConnect** 来浏览 SQL Server 的驱动程序可用的连接。 首先，应用程序请求连接句柄：  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 接下来，应用程序调用 **SQLBrowseConnect** ，并使用 **SQLDrivers**返回的驱动程序描述指定 SQL Server 驱动程序：  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 由于这是对 **SQLBrowseConnect**的首次调用，驱动程序管理器将加载 SQL Server 驱动程序，并将该驱动程序的 **SQLBrowseConnect** 函数与从应用程序接收的参数相同。  
  
> [!NOTE]  
>  如果要连接到支持 Windows 身份验证的数据源提供程序，应 `Trusted_Connection=yes` 在连接字符串中指定而不是用户 ID 和密码信息。  
  
 驱动程序确定这是首次调用 **SQLBrowseConnect** ，并返回第二级连接属性：服务器、用户名、密码、应用程序名称和工作站 ID。 对于 server 属性，它将返回有效服务器名称的列表。 **SQLBrowseConnect**中的返回代码是 SQL_NEED_DATA。 下面是浏览结果字符串：  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 浏览结果字符串中的每个关键字后跟一个冒号和一个或多个位于等号前面的单词。 这些词是应用程序可用于构建对话框的用户友好名称。 **应用**和**WSID**关键字以星号作为前缀，这意味着这些关键字是可选的。 **SERVER**、 **UID**和**PWD**关键字不带有星号前缀;必须在下一个浏览请求字符串中为其提供值。 **服务器**关键字的值可以是**SQLBrowseConnect**返回的服务器之一，也可以是用户提供的名称。  
  
 应用程序再次调用 **SQLBrowseConnect** ，指定绿色服务器，并在每个关键字后面省略 **应用程序** 和 **WSID** 关键字以及用户友好名称：  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 驱动程序尝试连接到绿色服务器。 如果存在任何非致命错误（如缺少关键字-值对），则 **SQLBrowseConnect** 将返回 SQL_NEED_DATA，并保持与错误之前相同的状态。 应用程序可以调用 **SQLGetDiagField** 或 **SQLGetDiagRec** 来确定错误。 如果连接成功，则驱动程序将返回 SQL_NEED_DATA 并返回浏览结果字符串：  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 由于此字符串中的属性是可选的，因此应用程序可以省略它们。 但是，应用程序必须再次调用 **SQLBrowseConnect** 。 如果应用程序选择省略数据库名称和语言，则它指定一个空的浏览请求字符串。 在此示例中，应用程序选择 pubs 数据库，并在最后一次调用**SQLBrowseConnect** ，并在**database**关键字之前省略**LANGUAGE**关键字和星号：  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 由于 **数据库** 属性是驱动程序所需的最终连接属性，因此浏览过程已完成，应用程序连接到数据源，而 **SQLBrowseConnect** 返回 SQL_SUCCESS。 **SQLBrowseConnect** 还将完整的连接字符串作为浏览结果字符串返回：  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 驱动程序返回的最终连接字符串不包含每个关键字后面的用户友好名称，也不包含应用程序未指定的可选关键字。 当断开) 或连接到其他连接句柄上的数据源之后，应用程序可以将此字符串与 **SQLDriverConnect** 一起使用，以重新连接到当前连接句 (柄上的数据源。 例如：  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
