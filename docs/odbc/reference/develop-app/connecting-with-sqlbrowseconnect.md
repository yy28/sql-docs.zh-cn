---
title: "使用 SQLBrowseConnect 连接 |Microsoft 文档"
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
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 95e44aef6839d219dd06523baef8d0d0be3ebe41
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="connecting-with-sqlbrowseconnect"></a>使用 SQLBrowseConnect 连接
**SQLBrowseConnect**、 like **SQLDriverConnect**，使用的连接字符串。 但是，通过使用**SQLBrowseConnect**，应用程序可以在运行时构造完整连接字符串。 这允许应用程序执行以下两种操作：  
  
-   生成其自己的对话框，提示输入此信息，从而保留控制其"外观和感觉。"  
  
-   浏览系统以找到可由特定的驱动程序使用的数据源，这可能要执行若干步骤。 例如，用户可能要首先浏览网络以找到服务器，然后在选择某一服务器后，浏览该服务器以找到驱动程序可访问的数据库。  
  
 应用程序调用**SQLBrowseConnect**并将传递连接字符串，称为*浏览请求连接字符串，* ，指定驱动程序或数据源。 该驱动程序返回的连接字符串，称为*浏览结果连接字符串，*包含关键字，可能的值 （如果关键字接受一组离散的值），和用户友好名称。 应用程序生成的用户友好名称与一个对话框，并提示用户输入值。 然后生成一个新的浏览请求连接字符串从这些值并返回此到通过再次调用该驱动程序**SQLBrowseConnect**。  
  
 由于来回传递连接字符串，该驱动程序可以提供多个级别的浏览通过应用程序返回旧时返回一个新的连接字符串。 例如，应用程序调用的第一次**SQLBrowseConnect**，驱动程序可能会返回关键字来提示用户输入服务器名称。 当应用程序返回服务器名称时，该驱动程序可能会返回关键字来提示用户输入数据库。 应用程序返回的数据库名称后，浏览过程将会完成。  
  
 每次**SQLBrowseConnect**返回新的浏览结果连接字符串，它将返回 SQL_NEED_DATA 作为其返回代码。 这将告知应用程序连接过程不完整。 直到**SQLBrowseConnect** SQL_SUCCESS，连接将返回处于一种需要数据状态并不能用于其他目的，如设置连接属性。 应用程序可以终止连接浏览过程，通过调用**SQLDisconnect**。  
  
 本部分包含以下主题。  
  
-   [SQL Server 浏览示例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
