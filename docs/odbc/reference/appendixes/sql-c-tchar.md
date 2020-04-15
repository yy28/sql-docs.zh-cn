---
title: SQL_C_TCHAR |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304068"
---
# <a name="sql_c_tchar"></a>SQL_C_TCHAR
SQL_C_TCHAR类型标识符实际上不标识数据类型;因此，该标识符实际上不会标识数据类型。它是存在在 Unicode 转换的标头文件中的宏。 它替换为SQL_C_CHAR或SQL_C_WCHAR，具体取决于 UNICODE **#define**的设置。 它对于传输字符数据的应用程序非常有用，这些数据被编译为 ANSI 和 Unicode 应用程序。
