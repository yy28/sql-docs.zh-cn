---
title: 使用 SQLDriverConnect 连接 |Microsoft 文档
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be52bf2e14316c63b417563d0ccf829d7413ff11
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
