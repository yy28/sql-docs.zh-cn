---
title: 使用 SQLBrowseConnect 连接 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04df089b97bf385925c87a98b3f89cdac3ef21e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083132"
---
# <a name="connecting-with-sqlbrowseconnect"></a>使用 SQLBrowseConnect 连接
**SQLBrowseConnect**，例如**SQLDriverConnect**，使用连接字符串。 但是，通过使用**SQLBrowseConnect**，应用程序可以在运行时构造完整连接字符串。 这允许应用程序执行以下两种操作：  
  
-   生成其自己的对话框来提示输入此信息，从而保持控制其"外观和感觉。"  
  
-   浏览系统以找到可由特定的驱动程序使用的数据源，这可能要执行若干步骤。 例如，用户可能要首先浏览网络以找到服务器，然后在选择某一服务器后，浏览该服务器以找到驱动程序可访问的数据库。  
  
 应用程序调用**SQLBrowseConnect** ，并将传递连接字符串，称为*浏览请求连接字符串，* 指定驱动程序或数据源。 该驱动程序返回的连接字符串，称为*浏览结果连接字符串中，* 包含关键字，可能的值 （如果关键字接受一组离散的值），和用户友好的名称。 应用程序生成具有用户友好名称的对话框，并提示用户输入的值。 然后生成一个新的浏览请求连接字符串从这些值并返回此驱动程序和另一个调用到**SQLBrowseConnect**。  
  
 因为来回传递连接字符串，该驱动程序可以提供浏览时应用程序返回旧返回新的连接字符串的多个级别。 例如，应用程序调用的第一次**SQLBrowseConnect**，则驱动程序可能返回的关键字以提示用户输入服务器名称。 当应用程序返回的服务器名称时，驱动程序可能会返回关键字来提示用户输入一个数据库。 应用程序返回数据库名称后，浏览过程会完成。  
  
 每次**SQLBrowseConnect**返回新的浏览结果连接字符串，它将返回它的返回代码为 SQL_NEED_DATA。 这将告知应用程序的连接过程未完成。 直到**SQLBrowseConnect**返回 SQL_SUCCESS，该连接处于一种需要数据状态，不能用于其他目的，例如若要设置连接属性。 应用程序可以终止连接浏览进程通过调用**SQLDisconnect**。  
  
 本部分包含以下主题。  
  
-   [SQL Server 浏览示例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
