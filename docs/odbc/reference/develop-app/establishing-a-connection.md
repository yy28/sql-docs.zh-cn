---
title: 建立连接 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f71190a8a2ca1dd8af0d28adb5531540fb1b57e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298697"
---
# <a name="establishing-a-connection"></a>建立连接
在分配环境和连接句柄并设置任何连接属性后，应用程序已准备好连接到数据源或驱动程序。 应用程序可以使用三种不同的功能 **：SQLConnect（** 核心接口一致性级别 **）、SQLDriverConnect（** 核心）和**SQLBrowseConnect（** 级别 1）。 这三者中的每一个都设计为在不同的场景中使用。 在连接之前，应用程序可以确定 SQLDrivers 返回的**ConnectFunctions**关键字支持这些函数中的**哪一**个。  
  
> [!NOTE]  
>  某些驱动程序限制其支持的活动连接数。 应用程序使用SQL_MAX_DRIVER_CONNECTIONS选项调用**SQLGetInfo，** 以确定特定驱动程序支持多少活动连接。  
  
 本部分包含以下主题。  
  
-   [默认数据源](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [使用 SQLConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [连接字符串](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [使用 SQLDriverConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [使用 SQLBrowseConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
