---
title: 桌面数据库驱动程序兼容性 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5fb1e93c996b68a3110449dab797beb5c93208b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32899762"
---
# <a name="desktop-database-driver-compatibility"></a>桌面数据库驱动程序兼容性
Unicode 是一种软件字符编码的方法将所有字符视为有固定的宽度的两个字节。 此方法用于替代为 Windows ANSI 字符编码，即，因为它表示为一个字节中的字符限制为 256 个字符。 因为 Unicode 可以代表 65000 字符，它还包含许多语言的字符不表示以 ANSI 编码。  
  
 ODBC 3.5 （或更高版本） 驱动程序管理器完全支持 Unicode。 这会影响两个主要区域： 函数调用和字符串数据类型。 驱动程序管理器映射函数字符串自变量和所需的应用程序和驱动程序的字符串数据，这两种可以是 Unicode 启用或 ANSI 已启用。  
  
 ODBC 3.5 （或更高版本） 驱动程序管理器支持使用 Unicode 应用程序和 ANSI 应用程序的 Unicode 驱动程序使用。 它还支持使用与 ANSI 应用程序的 ANSI 驱动程序。 驱动程序管理器提供了有限的 Unicode ANSI 映射为 Unicode 应用程序使用 ANSI 驱动程序。 这允许访问的 Jet 3.5 数据库和所有现有 ISAM 文件类型的支持。  
  
 当 ANSI 应用程序使用 ODBC 桌面数据库驱动程序 4.0 和访问 Microsoft 访问 4.0 或更高版本，该驱动程序的数据类型将作为公开 SQL_CHAR、 SQL_VARCHAR 或 SQL_LONGVARCHAR 即使 Jet 4.0 支持的宽版本。 较旧版本的 Jet 不支持 SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 在其中使用 Jet 4.0 数据库引擎使用的旧格式的情况下，此限制也适用。  
  
 有关 ODBC Unicode 问题的详细信息，请参阅[Unicode](../../odbc/reference/develop-app/unicode.md)中编程注意事项。
