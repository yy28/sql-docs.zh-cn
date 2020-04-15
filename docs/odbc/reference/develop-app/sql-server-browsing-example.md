---
title: SQL 服务器浏览示例 |微软文档
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
ms.openlocfilehash: 7b15aa8e3d573660a312fceb5b9100a41f0384d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301978"
---
# <a name="sql-server-browsing-example"></a>SQL Server 浏览示例
下面的示例演示如何使用**SQLBrowseConnect**来浏览 SQL Server 驱动程序可用的连接。 首先，应用程序请求连接句柄：  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 接下来，应用程序调用**SQLBrowseConnect**并指定 SQL Server 驱动程序，使用**SQLDriver**返回的驱动程序说明 ：  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 由于这是第一次调用**SQLBrowseConnect，** 驱动程序管理器加载 SQL Server 驱动程序，并且使用从应用程序接收的相同参数调用驱动程序的**SQLBrowseConnect**函数。  
  
> [!NOTE]  
>  如果要连接到支持 Windows 身份验证的数据源提供程序，则应在连接字符串中指定`Trusted_Connection=yes`而不是用户 ID 和密码信息。  
  
 驱动程序确定这是对**SQLBrowseConnect**的第一次调用，并返回第二级连接属性：服务器、用户名、密码、应用程序名称和工作站 ID。 对于服务器属性，它返回有效服务器名称的列表。 **SQLBrowseConnect**的返回代码SQL_NEED_DATA。 下面是浏览结果字符串：  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 浏览结果字符串中的每个关键字后面跟一个冒号和等于符号前的一个或多个单词。 这些单词是应用程序可用于生成对话框的用户友好名称。 **APP**和**WSID**关键字由星号预缀，这意味着它们是可选的。 **服务器****、UID**和**PWD**关键字不由星号预缀;必须在下一个浏览请求字符串中为它们提供值。 **SERVER**关键字的值可能是**SQLBrowseConnect**返回的服务器之一或用户提供的名称。  
  
 应用程序再次调用**SQLBrowseConnect，** 指定绿色服务器，并省略**APP**和**WSID**关键字以及每个关键字后的用户友好名称：  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 驱动程序尝试连接到绿色服务器。 如果存在任何非致命错误（如缺少关键字值对 **），SQLBrowseConnect**将返回SQL_NEED_DATA并保留与错误之前相同的状态。 应用程序可以调用**SQLGetDiagField**或**SQLGetDiagRec**来确定错误。 如果连接成功，驱动程序将返回SQL_NEED_DATA并返回浏览结果字符串：  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 由于此字符串中的属性是可选的，因此应用程序可以省略它们。 但是，应用程序必须再次调用**SQLBrowseConnect。** 如果应用程序选择省略数据库名称和语言，它将指定一个空浏览请求字符串。 在此示例中，应用程序选择 pubs 数据库并调用**SQLBrowseConnect**进行最后一次，省略**了语言**关键字和**DATABASE**关键字前的星号：  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 由于**DATABASE**属性是驱动程序所需的最终连接属性，因此浏览过程已完成，应用程序已连接到数据源 **，SQLBrowseConnect**返回SQL_SUCCESS。 **SQLBrowseConnect**还会将完整的连接字符串作为浏览结果字符串返回：  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 驱动程序返回的最终连接字符串不包含每个关键字之后的用户友好名称，也不包含应用程序未指定的可选关键字。 应用程序可以使用此字符串与**SQLDriverConnect**重新连接到当前连接句柄上的数据源（断开连接后），或连接到其他连接句柄上的数据源。 例如：  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
