---
description: 使用 SQLBrowseConnect 连接
title: 与 SQLBrowseConnect 连接 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7ad54276f54155c68fbdbe984642dda4300a7c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424819"
---
# <a name="connecting-with-sqlbrowseconnect"></a>使用 SQLBrowseConnect 连接
**SQLBrowseConnect**（如 **SQLDriverConnect**）使用连接字符串。 但是，通过使用 **SQLBrowseConnect**，应用程序可以在运行时构造完整的连接字符串。 这允许应用程序执行以下两种操作：  
  
-   构建自己的对话框以提示输入此信息，从而保持对其 "外观" 的控制。  
  
-   浏览系统以找到可由特定的驱动程序使用的数据源，这可能要执行若干步骤。 例如，用户可能要首先浏览网络以找到服务器，然后在选择某一服务器后，浏览该服务器以找到驱动程序可访问的数据库。  
  
 应用程序调用 **SQLBrowseConnect** 并传递一个连接字符串（称为 " *浏览请求连接字符串"）* ，该字符串指定驱动程序或数据源。 驱动程序返回一个连接字符串（称为 " *浏览结果连接字符串"）* ，其中包含关键字、可能的值 (如果关键字接受一组离散的值) 和用户友好名称。 应用程序将生成一个具有用户友好名称的对话框，并提示用户输入值。 然后从这些值生成新的浏览请求连接字符串，并将其返回给驱动程序，同时调用 **SQLBrowseConnect**。  
  
 由于连接字符串会来回传递，因此，驱动程序可以在应用程序返回旧的连接字符串时，通过返回新的连接字符串来提供多个级别的浏览。 例如，当应用程序第一次调用 **SQLBrowseConnect**时，驱动程序可能返回关键字以提示用户输入服务器名称。 当应用程序返回服务器名称时，驱动程序可能返回关键字以提示用户输入数据库。 在应用程序返回数据库名称后，浏览过程将会完成。  
  
 每次 **SQLBrowseConnect** 返回一个新的浏览结果连接字符串时，它会返回 SQL_NEED_DATA 作为其返回代码。 这会告知应用程序连接过程不完整。 在 **SQLBrowseConnect** 返回 SQL_SUCCESS 之前，连接处于需要数据状态，不能用于其他目的，例如设置连接属性。 应用程序可以通过调用 **SQLDisconnect**来终止连接浏览进程。  
  
 本部分包含以下主题。  
  
-   [SQL Server 浏览示例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
