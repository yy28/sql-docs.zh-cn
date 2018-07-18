---
title: Unicode 数据 |Microsoft 文档
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
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee404891b20f721cec0ea9e56b9eab1e78ad6f8f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915812"
---
# <a name="unicode-data"></a>Unicode 数据
SQL Unicode 数据类型用于描述驻留在本机上 DBMS 为 Unicode 的数据。 C Unicode 数据类型可用于允许应用程序将数据绑定到 Unicode 缓冲区。 驱动程序管理器可以将数据转换从 Unicode C 类型 (SQL_C_WCHAR) 以使其带有 ANSI 驱动程序的函数。  
  
 ODBC 3.0 或 2。*x*应用程序总是绑定到的 ANSI 数据类型。 为了获得最佳性能，ODBC 3.5 （或更高版本） 应用程序应绑定到 ANSI C 数据类型中，如果 SQL 列类型是 ANSI，并且应绑定到 Unicode C 数据类型，如果 SQL 列类型采用 unicode 编码。  
  
 SQL Unicode 类型指示器是 SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 SQL_WCHAR 数据都具有固定的字符串长度，而 SQL_WVARCHAR 具有可变长度与声明的最大值和 SQL_WLONGVARCHAR 具有可变长度取决于数据源最多。  
  
 C Unicode 类型指示符是 SQL_C_WCHAR。 这是默认值为每个 SQL Unicode 类型指示器。 所有 SQL 类型可转换为 SQL_C_WCHAR 和 SQL_C_WCHAR 可以转换为所有 SQL 类型。 应用程序可以检索以下三种方式中的数据：  
  
-   为 SQL_C_CHAR 检索数据。  
  
-   为 SQL_C_WCHAR 检索数据。  
  
-   将数据作为 SQL_C_TCHAR 声明。 这是插入 SQL_C_WCHAR，如果应用程序编译为 Unicode 应用程序，或者插入 SQL_C_CHAR，如果它被编译成 ANSI 应用程序的宏。  
  
 SQL_C_TCHAR，如下所示的函数中声明：  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 当应用程序编译为 Unicode 应用程序， *ValueType*自变量将从 SQL_C_TCHAR 更改为 SQL_C_WCHAR。 当应用程序编译为 ANSI 应用程序， *ValueType*自变量将更改为 SQL_C_CHAR。  
  
 Unicode 驱动程序必须仍支持 ANSI 数据类型，包括 SQL_CHAR。 如果使用 Unicode 驱动程序的应用程序绑定到 SQL_CHAR，驱动程序管理器将不映射到 SQL_WCHAR SQL_CHAR 数据。 Unicode 驱动程序必须接受 SQL_CHAR 数据。  
  
 驱动程序管理器将驱动程序和 DSN 名称存储在 Unicode，并将它们映射到 ANSI，根据需要。 如果一个 Unicode 字符不能映射到一个 ANSI 字符 （如会出现在驱动程序和 DSN 名称中使用了不是计算机的本机代码页的代码页从字符），由默认字符 sup 表示无法转换的字符plied 系统。
