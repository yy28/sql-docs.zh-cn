---
title: 建立连接 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establishing a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establishing a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7ef6f3d50382d810dd9df246c4d857d9467674f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "76941028"
---
# <a name="establishing-a-connection"></a>建立连接
分配环境和连接句柄并设置任何连接属性后，应用程序就可以连接到数据源或驱动程序了。 应用程序可以使用三种不同的函数来执行此操作： **SQLConnect** （核心接口一致性级别）、 **SQLDriverConnect** （core）和**SQLBrowseConnect** （级别1）。 这三种方案中的每一个都设计为在不同的方案中使用。 在连接之前，应用程序可以通过**SQLDrivers**返回的**ConnectFunctions**关键字来确定支持这些函数中的哪一个。  
  
> [!NOTE]  
>  某些驱动程序会限制它们支持的活动连接数。 应用程序使用 SQL_MAX_DRIVER_CONNECTIONS 选项调用**SQLGetInfo** ，以确定特定驱动程序支持的活动连接数。  
  
 本部分包含下列主题。  
  
-   [默认数据源](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [使用 SQLConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [连接字符串](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [使用 SQLDriverConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [使用 SQLBrowseConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
