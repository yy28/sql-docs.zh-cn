---
title: "SQL_C_TCHAR |Microsoft 文档"
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
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 63c23a242b7acd7dd3cf10acb3f60dea980cd398
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
SQL_C_TCHAR 类型标识符不真正标识一种数据类型;它是 Unicode 转换标头文件中存在的宏。 它根据 UNICODE 设置替换为 SQL_C_CHAR 或 SQL_C_WCHAR **#define**。 它可用于应用程序将编译为 ANSI 和 Unicode 应用程序的字符数据传输。
