---
title: 桌面数据库驱动程序兼容性 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89eea7ab112eaefdc73c7cbc72ee3555797c7efd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303518"
---
# <a name="desktop-database-driver-compatibility"></a>桌面数据库驱动程序兼容性
Unicode 是一种软件字符编码方法，它将所有字符视为具有两个字节的固定宽度。 此方法用作 Windows ANSI 字符编码的替代方法，由于它表示一个字节中的字符，因此限制为 256 个字符。 由于 Unicode 可以表示超过 65，000 个字符，因此它适合许多字符在 ANSI 编码中未表示的语言。  
  
 ODBC 3.5（或更高版本）驱动程序管理器已启用 Unicode。 这会影响两个主要区域：函数调用和字符串数据类型。 驱动程序管理器根据应用程序和驱动程序的要求映射函数字符串参数和字符串数据，这两个参数都可以启用 Unicode 或启用 ANSI。  
  
 ODBC 3.5（或更高版本）驱动程序管理器支持将 Unicode 驱动程序与 Unicode 应用程序和 ANSI 应用程序一起使用。 它还支持将 ANSI 驱动程序与 ANSI 应用程序一起使用。 驱动程序管理器为使用 ANSI 驱动程序的 Unicode 应用程序提供有限的 Unicode 到 ANSI 映射。 这允许访问 Jet 3.5 数据库并支持所有现有的 ISAM 文件类型。  
  
 当 ANSI 应用程序使用 ODBC 桌面数据库驱动程序 4.0 并访问 Microsoft Access 4.0 或更高版本时，驱动程序将数据类型公开为SQL_CHAR、SQL_VARCHAR或SQL_LONGVARCHAR，即使 Jet 4.0 支持宽版本。 旧版本的 Jet 不支持SQL_WCHAR、SQL_WVARCHAR和SQL_WLONGVARCHAR。 此限制也适用于旧格式与 Jet 4.0 数据库引擎一起使用的情况。  
  
 有关 ODBC 的 Unicode 问题的详细信息，请参阅编程注意事项中的[Unicode。](../../odbc/reference/develop-app/unicode.md)
