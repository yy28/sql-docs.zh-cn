---
title: "连接句柄 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba20d3fcb6d943f4669774013dcb62c8ad896d8d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connection-handles"></a>连接句柄
A*连接*组成驱动程序和数据源。 连接句柄标识每个连接。 连接句柄定义要使用的驱动程序不仅要使用该驱动程序使用的数据源。 实现 ODBC （驱动程序管理器或驱动程序） 的代码段，在连接句柄标识包含连接信息，如下所示的结构：  
  
-   连接的状态  
  
-   当前的连接级别诊断  
  
-   语句和当前连接上分配的描述符句柄  
  
-   每个连接属性的当前设置  
  
 ODBC 不能防止多个并发连接，如果驱动程序支持它们。 因此，在特定 ODBC 环境中，多个连接句柄可能指向各种驱动程序和数据源，到相同的驱动程序和不同的数据源，或甚至到多个连接到相同的驱动程序和数据源。 某些驱动程序限制它们支持; 的活动连接数SQL_MAX_DRIVER_CONNECTIONS 选项**SQLGetInfo**指定特定驱动程序支持的活动连接数。  
  
 连接到数据源时，主要用于连接句柄 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**)，正在断开连接的数据源 (**SQLDisconnect**)，获取有关的驱动程序和数据源的信息 (**SQLGetInfo**)，检索诊断 (**SQLGetDiagField**和**SQLGetDiagRec**)，并执行事务 (**SQLEndTran**)。 也用于设置和获取连接属性时 (**SQLSetConnectAttr**和**SQLGetConnectAttr**) 和获取 SQL 语句的本机格式时 (**SQLNativeSql**).  
  
 连接句柄分配与**SQLAllocHandle**并释放与**SQLFreeHandle**。
