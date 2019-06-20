---
title: Unicode 数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74de6c44aaf109a434f0cf76c6902abfba92efe1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305772"
---
# <a name="unicode-data"></a>Unicode 数据
提供 SQL Unicode 数据类型来描述驻留在本机上 DBMS 为 Unicode 的数据。 提供一种 C Unicode 数据类型以使应用程序将数据绑定到 Unicode 缓冲区。 驱动程序管理器可以将数据从 Unicode C 类型 (SQL_C_WCHAR) 以使其转换函数使用 ANSI 驱动程序。  
  
 ODBC 3.0 或 2。*x*应用程序将始终绑定到的 ANSI 数据类型。 为获得最佳性能，ODBC 3.5 （或更高版本） 应用程序应绑定到 ANSI C 数据类型中，如果 SQL 列类型为 ANSI，并应将绑定到 Unicode C 数据类型 SQL 列类型是否为 Unicode。  
  
 SQL Unicode 类型指示符为 SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 SQL_WCHAR 数据有固定的字符串的长度，而 SQL_WVARCHAR 具有可变长度的声明的最大值和 SQL_WLONGVARCHAR 具有可变长度取决于数据源的最大值。  
  
 C Unicode 类型指示符是 SQL_C_WCHAR。 这是默认值为每个 SQL Unicode 类型指示符。 所有 SQL 类型可以转换为 sql_c_wchar; 和 SQL_C_WCHAR 可以转换为的所有 SQL 类型。 应用程序可以检索数据中有以下三种：  
  
-   检索为 SQL_C_CHAR 数据。  
  
-   像 sql_c_wchar 一样检索数据。  
  
-   将数据声明为 SQL_C_TCHAR。 这是一个宏来插入 SQL_C_WCHAR，如果应用程序编译为 Unicode 应用程序，或者插入 SQL_C_CHAR，如果它被编译成 ANSI 应用程序。  
  
 SQL_C_TCHAR，如下所示的函数中声明：  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 当应用程序编译为 Unicode 应用程序， *ValueType*参数将更改从 SQL_C_TCHAR 为 SQL_C_WCHAR。 在作为 ANSI 应用程序，编译应用程序时*ValueType*参数将更改为 SQL_C_CHAR。  
  
 Unicode 驱动程序必须仍支持 ANSI 数据类型，包括 SQL_CHAR。 如果使用 Unicode 驱动程序的应用程序绑定到 SQL_CHAR，驱动程序管理器将映射到 SQL_WCHAR SQL_CHAR 数据。 Unicode 驱动程序必须接受 SQL_CHAR 数据。  
  
 驱动程序管理器以 Unicode 存储驱动程序和 DSN 名称，并根据需要将它们映射为 ANSI。 如果 Unicode 字符不能映射为 ANSI 字符 （如可以发生，如果不是计算机的本机代码页的代码页中的字符用在驱动程序和 DSN 名称），由默认字符 sup 表示无法转换的字符plied 系统。
