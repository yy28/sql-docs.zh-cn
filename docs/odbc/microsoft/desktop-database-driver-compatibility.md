---
title: 桌面数据库驱动程序兼容性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31263162526b6bd2e0a116a473f09f9e2caeba94
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077286"
---
# <a name="desktop-database-driver-compatibility"></a>桌面数据库驱动程序兼容性
Unicode 是一种软件字符编码的方法将所有字符视为有两个字节的固定的宽度。 此方法用作到 Windows ANSI 字符编码，即，因为它表示一个字节中的字符超过 256 个字符的替代方法。 Unicode 可表示 65,000 多个字符，因为它可以包括许多语言的字符可能不会以 ANSI 编码。  
  
 ODBC 3.5 （或更高版本） 驱动程序管理器完全支持 Unicode。 这会影响两个主要领域： 函数调用，并且字符串数据类型。 驱动程序管理器映射函数的字符串参数和所需的应用程序和驱动程序的字符串数据，这两种可以是支持 Unicode 或 ANSI 已启用。  
  
 ODBC 3.5 （或更高版本） 驱动程序管理器支持 Unicode 驱动程序使用 Unicode 应用程序和 ANSI 应用程序的使用。 它还支持使用 ANSI 应用程序的 ANSI 驱动程序使用。 驱动程序管理器提供了有限的 Unicode 到 ANSI 映射为 Unicode 应用程序使用 ANSI 驱动程序。 这允许访问的 Jet 3.5 数据库和所有现有 ISAM 文件类型的支持。  
  
 当 ANSI 应用程序使用 ODBC 桌面数据库驱动程序 4.0 和访问 Microsoft 访问 4.0 或更高版本，该驱动程序的数据类型将作为公开 SQL_CHAR、 SQL_VARCHAR 或 SQL_LONGVARCHAR 即使 Jet 4.0 支持宽版本。 SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR 不支持较旧版本的 Jet。 在与 Jet 4.0 数据库引擎使用旧格式的位置的情况下，此限制也适用。  
  
 有关使用 ODBC Unicode 问题的详细信息，请参阅[Unicode](../../odbc/reference/develop-app/unicode.md)编程注意事项。
