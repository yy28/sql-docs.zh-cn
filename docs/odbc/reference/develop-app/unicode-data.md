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
ms.openlocfilehash: 899924b5c0847d5f42e383a9e04c33298bb368b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087747"
---
# <a name="unicode-data"></a>Unicode 数据
提供了 SQL Unicode 数据类型，用于描述本机上以 Unicode 格式保存的数据。 提供 C Unicode 数据类型，使应用程序可以将数据绑定到 Unicode 缓冲区。 驱动程序管理器可以转换 Unicode C 类型（SQL_C_WCHAR）中的数据，使其与 ANSI 驱动程序一起工作。  
  
 ODBC 3.0 或2。*x*应用程序将始终绑定到 ANSI 数据类型。 为了获得最佳性能，如果 SQL 列类型为 ANSI，ODBC 3.5 （或更高版本）应用程序应绑定到 ANSI data C 类型，如果 SQL 列类型为 Unicode，则应绑定到 Unicode C 数据类型。  
  
 SQL Unicode 类型指示器是 SQL_WCHAR、SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 SQL_WCHAR 数据具有固定字符串长度，而 SQL_WVARCHAR 的可变长度为已声明的最大值，SQL_WLONGVARCHAR 的长度可变，且最大值取决于数据源。  
  
 C Unicode 类型指示器 SQL_C_WCHAR。 这是每个 SQL Unicode 类型指示器的默认值。 所有 SQL 类型都可以转换为 SQL_C_WCHAR，SQL_C_WCHAR 可转换为所有 SQL 类型。 应用程序可以通过以下三种方式之一来检索数据：  
  
-   检索 SQL_C_CHAR 数据。  
  
-   检索 SQL_C_WCHAR 数据。  
  
-   将数据声明为 SQL_C_TCHAR。 这是一个宏，如果将应用程序编译为 Unicode 应用程序 SQL_C_CHAR 或将其编译为 ANSI 应用程序，则插入 SQL_C_WCHAR。  
  
 在函数中声明 SQL_C_TCHAR，如下所示：  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 当应用程序编译为 Unicode 应用程序时， *ValueType*参数将从 SQL_C_TCHAR 更改为 SQL_C_WCHAR。 当应用程序编译为 ANSI 应用程序时， *ValueType*参数将更改为 SQL_C_CHAR。  
  
 Unicode 驱动程序必须仍支持 ANSI 数据类型，包括 SQL_CHAR。 如果使用 Unicode 驱动程序的应用程序绑定到 SQL_CHAR，则驱动程序管理器不会将 SQL_CHAR 数据映射到 SQL_WCHAR。 Unicode 驱动程序必须接受 SQL_CHAR 的数据。  
  
 驱动程序管理器将驱动程序和 DSN 名称按 Unicode 存储，并根据需要将它们映射到 ANSI。 如果 Unicode 字符不能映射到 ANSI 字符（如在驱动程序和 DSN 名称中使用了不是计算机的本机代码页的代码页中的字符，则可能会出现这种情况），则不能转换的字符由默认字符 sup 表示plied 系统。
