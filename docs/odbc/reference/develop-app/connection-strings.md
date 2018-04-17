---
title: 连接字符串 |Microsoft 文档
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
- connecting to driver [ODBC], connection strings
- functions [ODBC], data source or driver connections
- connection strings [ODBC], about connection strings
- connecting to data source [ODBC], connection strings
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: 724c7b86-300a-4fa9-ad96-4afa0fdcb3e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e48311df773abe0549ee447564c01a437bd0cca9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="connection-strings"></a>连接字符串
连接字符串包含用于建立的连接信息。 完整的连接字符串包含建立连接所需的所有信息。 连接字符串是一系列由分号分隔的关键字/值对。 (连接字符串的完整语法，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。)通过使用的连接字符串：  
  
-   **SQLDriverConnect**，这将完成的与用户交互的连接字符串。  
  
-   **SQLBrowseConnect**，这将完成以迭代方式与数据源的连接字符串。  
  
 **SQLConnect**不使用连接字符串; 使用**SQLConnect**类似于连接的连接字符串使用 3 个关键字/值对 (数据源名称和 （可选） 用户 ID 和密码).
