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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab8b94835fb9a6103436026a669c86f2401d57b0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036428"
---
# <a name="connection-handles"></a>连接句柄
一个*连接*组成一个驱动程序和数据源。 连接句柄标识每个连接。 连接句柄定义使用的驱动程序不仅要通过该驱动程序使用的数据源。 实现 ODBC （驱动程序管理器或驱动程序） 的代码段，在连接句柄标识结构，其中包含连接信息，如下所示：  
  
-   连接的状态  
  
-   当前的连接级别诊断  
  
-   语句和描述符在连接上当前分配的句柄  
  
-   每个连接属性的当前设置  
  
 ODBC 不会阻止多个并发连接，如果该驱动程序支持它们。 因此，在特定 ODBC 环境中，多个连接句柄可能指向各种驱动程序和数据源，到相同的驱动程序和各种数据源，或甚至到多个连接到相同的驱动程序和数据源。 某些驱动程序限制它们支持; 的活动连接数在选项 SQL_MAX_DRIVER_CONNECTIONS **SQLGetInfo**指定特定驱动程序支持的活动连接数。  
  
 连接到数据源时，主要用于连接句柄 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**)、 从数据断开连接源 (**SQLDisconnect**)，获取有关驱动程序和数据源的信息 (**SQLGetInfo**)，检索诊断 (**SQLGetDiagField**和**SQLGetDiagRec**)，并执行事务 (**SQLEndTran**)。 也用于设置和获取的连接属性时 (**SQLSetConnectAttr**并**SQLGetConnectAttr**) 和获取 SQL 语句的本机格式时 (**SQLNativeSql**).  
  
 分配连接句柄**SQLAllocHandle**和与已释放**SQLFreeHandle**。
