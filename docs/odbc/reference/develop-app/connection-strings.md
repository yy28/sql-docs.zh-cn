---
title: 连接字符串 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbbb5b4672a8ea393380063887cfd77b3e910238
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299027"
---
# <a name="connection-strings"></a>连接字符串
连接字符串包含用于建立连接的信息。 完整的连接字符串包含建立连接所需的所有信息。 连接字符串是一系列关键字/值对，由分号分隔。 （有关连接字符串的完整语法，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。连接字符串由以下者使用：  
  
-   **SQLDriverConnect**，它通过与用户的交互完成连接字符串。  
  
-   **SQLBrowseConnect**，它与数据源以迭代方式完成连接字符串。  
  
 SQLConnect 不使用连接字符串;因此 **，SQLConnect**不使用连接字符串。使用**SQLConnect**类似于使用仅包含三个关键字/值对的连接字符串（对于数据源名称，可选为用户 ID 和密码）。
