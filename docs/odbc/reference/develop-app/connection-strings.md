---
description: 连接字符串
title: 连接字符串 |Microsoft Docs
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
ms.openlocfilehash: fbb2d4b0c80a93b225bac754d2905b27e8844cbb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424769"
---
# <a name="connection-strings"></a>连接字符串
连接字符串包含用于建立连接的信息。 完整的连接字符串包含建立连接所需的所有信息。 连接字符串是一系列由分号分隔的关键字/值对。  (连接字符串的完整语法，请参阅 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 函数说明。 ) 使用连接字符串：  
  
-   **SQLDriverConnect**，它通过与用户交互来完成连接字符串。  
  
-   **SQLBrowseConnect**，它通过数据源迭代完成连接字符串。  
  
 **SQLConnect** 不使用连接字符串;使用 **SQLConnect** 类似于使用具有三个关键字/值对的连接字符串进行连接 (用于数据源名称和（可选）用户 ID 和密码) 。
