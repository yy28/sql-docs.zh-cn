---
title: "SQL_C_TCHAR |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b518868f3b6e77f9351877d57dc97cfee01a2c67
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlctchar"></a>SQL_C_TCHAR
SQL_C_TCHAR 类型标识符不真正标识一种数据类型;它是 Unicode 转换标头文件中存在的宏。 它根据 UNICODE 设置替换为 SQL_C_CHAR 或 SQL_C_WCHAR **#define**。 它可用于应用程序将编译为 ANSI 和 Unicode 应用程序的字符数据传输。
