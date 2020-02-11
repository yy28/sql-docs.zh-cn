---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 68a03de54a8a5f63a994578d64c6bce5a1279138
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057044"
---
# <a name="sql_c_tchar"></a>SQL_C_TCHAR
SQL_C_TCHAR 类型标识符实际上不标识数据类型;它是用于 Unicode 转换的标头文件中的宏。 根据 UNICODE **#define**的设置，它将替换为 SQL_C_CHAR 或 SQL_C_WCHAR。 它可用于传输同时编译为 ANSI 和 Unicode 应用程序的字符数据的应用程序。
