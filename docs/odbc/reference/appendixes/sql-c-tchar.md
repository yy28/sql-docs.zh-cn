---
description: SQL_C_TCHAR
title: SQL_C_TCHAR |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6fc7ff6e6334d49acc4e230b5fb12feb3f85556e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483170"
---
# <a name="sql_c_tchar"></a>SQL_C_TCHAR
SQL_C_TCHAR 类型标识符实际上不标识数据类型;它是用于 Unicode 转换的标头文件中的宏。 根据 UNICODE **#define**的设置，它将替换为 SQL_C_CHAR 或 SQL_C_WCHAR。 它可用于传输同时编译为 ANSI 和 Unicode 应用程序的字符数据的应用程序。
