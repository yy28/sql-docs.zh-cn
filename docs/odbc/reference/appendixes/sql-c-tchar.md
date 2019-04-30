---
title: SQL_C_TCHAR | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42afb911dda26cbda53f9cd14c883abb3775b94b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270528"
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
SQL_C_TCHAR 类型标识符不真正标识一种数据类型;它是在 Unicode 转换标头文件中存在一个宏。 它根据 UNICODE 的设置替换为 SQL_C_CHAR 或 SQL_C_WCHAR **#define**。 它可用于将字符数据作为 ANSI 和 Unicode 应用程序编译的应用程序。
