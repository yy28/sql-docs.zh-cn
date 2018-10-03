---
title: 建立的连接 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70f459f60616e7edd77078a7e9653ab9dff097e9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606368"
---
# <a name="establishing-a-connection"></a>建立连接
后分配环境和连接句柄并设置连接属性，该应用程序已准备好连接到数据源或驱动程序。 有三个应用程序可用于执行此操作的不同函数： **SQLConnect** （核心接口一致性级别）， **SQLDriverConnect** (Core) 和**SQLBrowseConnect**(级别 1)。 这三个用于在不同的方案中使用。 在连接时之前，应用程序可以确定这这些函数使用受支持**ConnectFunctions**返回的关键字**SQLDrivers**。  
  
> [!NOTE]  
>  某些驱动程序限制它们支持的活动连接数。 应用程序调用**SQLGetInfo** SQL_MAX_DRIVER_CONNECTIONS 选项以确定如何多个活动连接的特定驱动程序支持。  
  
 本部分包含以下主题。  
  
-   [默认数据源](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [使用 SQLConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [连接字符串](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [使用 SQLDriverConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [使用 SQLBrowseConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
