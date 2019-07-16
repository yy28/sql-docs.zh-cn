---
title: 使用 SQLDriverConnect 连接 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b8285ca9fddf0e1b77ca171414e4c00b0029d110
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036506"
---
# <a name="connecting-with-sqldriverconnect"></a>使用 SQLDriverConnect 连接
**SQLDriverConnect**用于连接到数据源使用的连接字符串。 **SQLDriverConnect**而不是使用**SQLConnect**原因如下：  
  
-   若要让应用程序使用特定于驱动程序的连接信息。  
  
-   请求驱动程序提示用户输入连接信息。  
  
-   若要连接而无需指定数据源。  
  
 本部分包含以下主题。  
  
-   [特定于驱动程序的连接信息](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [提示用户输入连接信息](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [使用文件数据源连接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [直接连接到驱动程序](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
