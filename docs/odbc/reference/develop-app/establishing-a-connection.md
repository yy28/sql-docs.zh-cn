---
title: 建立的连接 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establising a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establising a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 80de9f41bf4c535f7d9daa34b7b14d0377ab2383
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="establishing-a-connection"></a>建立连接
后分配环境和连接句柄并设置任何连接属性，应用程序已准备好连接到数据源或驱动程序。 应用程序可用于执行此操作的三个不同函数： **SQLConnect** （核心接口一致性级别）， **SQLDriverConnect** （核心） 和**SQLBrowseConnect**(级别 1)。 这三个用于在不同的方案中使用。 连接之前，，应用程序可以确定这这些函数与受支持**ConnectFunctions**关键字由**SQLDrivers**。  
  
> [!NOTE]  
>  某些驱动程序限制它们支持的活动连接数。 应用程序调用**SQLGetInfo** SQL_MAX_DRIVER_CONNECTIONS 选项，以确定如何多个活动连接特定的驱动程序支持。  
  
 本部分包含以下主题。  
  
-   [默认数据源](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [使用 SQLConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [连接字符串](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [使用 SQLDriverConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [使用 SQLBrowseConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
