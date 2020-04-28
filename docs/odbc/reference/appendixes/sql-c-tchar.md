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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 973d94b9b47371090a5f54fd3d259854ba78e9c2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304068"
---
# <a name="sql_c_tchar"></a>SQL_C_TCHAR
SQL_C_TCHAR 类型标识符实际上不标识数据类型;它是用于 Unicode 转换的标头文件中的宏。 根据 UNICODE **#define**的设置，它将替换为 SQL_C_CHAR 或 SQL_C_WCHAR。 它可用于传输同时编译为 ANSI 和 Unicode 应用程序的字符数据的应用程序。
