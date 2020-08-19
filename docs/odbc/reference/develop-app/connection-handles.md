---
description: 连接句柄
title: 连接句柄 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a4457fa72c40892e208057ac013d3da1e557a6d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424789"
---
# <a name="connection-handles"></a>连接句柄
*连接*包含驱动程序和数据源。 连接句柄标识每个连接。 连接句柄不仅定义要使用的驱动程序，而且还定义了要与该驱动程序一起使用的数据源。 在 (驱动程序管理器或驱动程序) 实现 ODBC 的代码段中，连接句柄标识包含连接信息的结构，如下所示：  
  
-   连接的状态  
  
-   当前连接级别诊断  
  
-   连接上当前分配的语句和描述符的句柄  
  
-   每个连接属性的当前设置  
  
 如果驱动程序支持多个连接，ODBC 不会阻止这些连接。 因此，在特定 ODBC 环境中，多个连接句柄可能指向各种驱动程序和数据源、同一驱动程序和不同的数据源，甚至是与同一驱动程序和数据源的多个连接。 某些驱动程序会限制它们支持的活动连接数; **SQLGetInfo** 中的 SQL_MAX_DRIVER_CONNECTIONS 选项指定特定驱动程序支持的活动连接数。  
  
 连接句柄主要用于连接到数据源 (**SQLConnect**、 **SQLDriverConnect**或 **SQLBrowseConnect**) 、断开与数据源的连接 (**SQLDisconnect**) 、获取有关驱动程序和数据源的信息 (**SQLGetInfo**) 、检索诊断 (**SQLGetDiagField** 和 **SQLGetDiagRec**) ，以及 (**SQLEndTran**) 执行事务。 在设置和获取 (**SQLSetConnectAttr** 和) **SQLGetConnectAttr** 的连接属性时，以及在获取 SQL 语句 (**SQLNativeSql**) 的本机格式时，它们也使用它们。  
  
 连接句柄通过 **SQLAllocHandle** 分配，并与 **SQLFreeHandle**一起释放。
