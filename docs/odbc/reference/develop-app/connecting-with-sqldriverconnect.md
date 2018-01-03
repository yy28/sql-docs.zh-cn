---
title: "使用 SQLDriverConnect 连接 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d9f6177b384da8866c8140cc30f1d32bca0bb635
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="connecting-with-sqldriverconnect"></a>使用 SQLDriverConnect 连接
**SQLDriverConnect**用于连接到数据源使用连接字符串。 **SQLDriverConnect**而不是使用**SQLConnect**原因如下：  
  
-   若要让应用程序使用特定于驱动程序的连接信息。  
  
-   请求驱动程序提示用户输入连接信息。  
  
-   若要连接，而指定的数据源。  
  
 本部分包含以下主题。  
  
-   [特定于驱动程序的连接信息](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [提示用户输入连接信息](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [使用文件数据源连接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [直接连接到驱动程序](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
