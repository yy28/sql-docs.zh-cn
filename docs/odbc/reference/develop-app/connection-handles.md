---
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
ms.openlocfilehash: d5b03e0733e35984350d2a218b885dc148ca8f8f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299017"
---
# <a name="connection-handles"></a>连接句柄
*连接*包含驱动程序和数据源。 连接句柄标识每个连接。 连接句柄不仅定义要使用的驱动程序，而且还定义了要与该驱动程序一起使用的数据源。 在实现 ODBC 的代码段（驱动程序管理器或驱动程序）内，连接句柄标识包含连接信息的结构，如下所示：  
  
-   连接的状态  
  
-   当前连接级别诊断  
  
-   连接上当前分配的语句和描述符的句柄  
  
-   每个连接属性的当前设置  
  
 如果驱动程序支持多个连接，ODBC 不会阻止这些连接。 因此，在特定 ODBC 环境中，多个连接句柄可能指向各种驱动程序和数据源、同一驱动程序和不同的数据源，甚至是与同一驱动程序和数据源的多个连接。 某些驱动程序会限制它们支持的活动连接数;**SQLGetInfo**中的 SQL_MAX_DRIVER_CONNECTIONS 选项指定特定驱动程序支持的活动连接数。  
  
 连接句柄主要用于连接到数据源（**SQLConnect**、 **SQLDriverConnect**或**SQLBrowseConnect**）、断开与数据源（**SQLDisconnect**）的连接、获取有关驱动程序和数据源（**SQLGetInfo**）的信息、检索诊断（**SQLGetDiagField**和**SQLGetDiagRec**）以及执行事务（**SQLEndTran**）。 在设置和获取连接属性（**SQLSetConnectAttr**和**SQLGetConnectAttr**）和获取 SQL 语句的本机格式（**SQLNativeSql**）时，也使用它们。  
  
 连接句柄通过**SQLAllocHandle**分配，并与**SQLFreeHandle**一起释放。
