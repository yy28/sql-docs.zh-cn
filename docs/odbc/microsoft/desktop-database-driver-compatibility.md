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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077286"
---
# <a name="desktop-database-driver-compatibility"></a>桌面数据库驱动程序兼容性
Unicode 是一种软件字符编码方法，将所有字符视为具有两个字节的固定宽度。 此方法用作 Windows ANSI 字符编码的替代方法，因为它表示一个字节中的字符，并且限制为256个字符。 因为 Unicode 可以表示超过65000个字符，所以它可以容纳许多语言，其字符不以 ANSI 编码表示。  
  
 ODBC 3.5 （或更高版本）驱动程序管理器启用了 Unicode。 这会影响两个主要方面：函数调用和字符串数据类型。 驱动程序管理器根据应用程序和驱动程序的需要映射函数字符串参数和字符串数据，两者都可以是启用了 Unicode 的或启用了 ANSI 的。  
  
 ODBC 3.5 （或更高版本）驱动程序管理器支持使用 unicode 驱动程序和 Unicode 应用程序。 它还支持将 ANSI 驱动程序与 ANSI 应用程序结合使用。 驱动程序管理器为使用 ANSI 驱动程序的 Unicode 应用程序提供了有限的 Unicode 到 ANSI 的映射。 这允许访问 Jet 3.5 数据库并支持所有现有的 ISAM 文件类型。  
  
 当 ANSI 应用程序使用 ODBC 桌面数据库驱动程序4.0 并访问 Microsoft Access 4.0 或更高版本时，驱动程序会将数据类型公开为 SQL_CHAR、SQL_VARCHAR 或 SQL_LONGVARCHAR，即使 Jet 4.0 支持广泛的版本。 旧版 Jet 不支持 SQL_WCHAR、SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 此限制也适用于旧格式与 Jet 4.0 数据库引擎一起使用的情况。  
  
 有关 ODBC 中的 Unicode 问题的详细信息，请参阅编程注意事项中的[unicode](../../odbc/reference/develop-app/unicode.md) 。
