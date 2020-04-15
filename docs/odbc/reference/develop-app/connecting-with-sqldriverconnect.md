---
title: 使用 SQLDriverConnect 连接 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6cd95364d8a5316a50d9f55616236a8677bf99e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299067"
---
# <a name="connecting-with-sqldriverconnect"></a>使用 SQLDriverConnect 连接
**SQLDriverConnect**用于使用连接字符串连接到数据源。 **SQLDriverConnect**的使用而不是**SQLConnect，** 原因如下：  
  
-   让应用程序使用特定于驱动程序的连接信息。  
  
-   请求驱动程序提示用户输入连接信息。  
  
-   在不指定数据源的情况下进行连接。  
  
 本部分包含以下主题。  
  
-   [特定于驱动程序的连接信息](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [提示用户输入连接信息](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [使用文件数据源连接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [直接连接到驱动程序](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
