---
title: Unicode 数据 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73ea9035b05f04fec1527ca2aa98531a807db8cf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307394"
---
# <a name="unicode-data"></a>Unicode 数据
提供 SQL Unicode 数据类型来描述驻留在 DBMS 上的 Unicode 本机数据。 提供了 C Unicode 数据类型，允许应用程序将数据绑定到 Unicode 缓冲区。 驱动程序管理器可以从 Unicode C 类型 （SQL_C_WCHAR） 转换数据，使其与 ANSI 驱动程序一起运行。  
  
 ODBC 3.0 或 2。*x*应用程序将始终绑定到 ANSI 数据类型。 为获得最佳性能，如果 SQL 列类型为 ANSI，则 ODBC 3.5（或更高）应用程序应绑定到 ANSI 数据类型，如果 SQL 列类型为 Unicode，则应绑定到 Unicode C 数据类型。  
  
 SQL Unicode 类型指示器SQL_WCHAR、SQL_WVARCHAR和SQL_WLONGVARCHAR。 SQL_WCHAR数据具有固定的字符串长度，而SQL_WVARCHAR具有具有声明最大值的可变长度，并且SQL_WLONGVARCHAR具有变量长度，最大值取决于数据源。  
  
 C Unicode 类型指示器SQL_C_WCHAR。 这是每个 SQL Unicode 类型指标的默认值。 所有 SQL 类型都可以转换为SQL_C_WCHAR，并且SQL_C_WCHAR可以转换为所有 SQL 类型。 应用程序可以通过三种方式之一检索数据：  
  
-   以SQL_C_CHAR身份检索数据。  
  
-   以SQL_C_WCHAR检索数据。  
  
-   将数据声明为SQL_C_TCHAR。 这是一个宏，用于插入SQL_C_WCHAR如果应用程序编译为 Unicode 应用程序，或者SQL_C_CHAR（如果应用程序编译为 ANSI 应用程序）插入。  
  
 SQL_C_TCHAR在函数中声明，如下所示：  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 当应用程序编译为 Unicode 应用程序时 *，ValueType*参数将从SQL_C_TCHAR更改为SQL_C_WCHAR。 当应用程序编译为 ANSI 应用程序时 *，ValueType*参数将更改为SQL_C_CHAR。  
  
 Unicode 驱动程序仍必须支持 ANSI 数据类型，包括SQL_CHAR。 如果使用 Unicode 驱动程序的应用程序绑定到SQL_CHAR，驱动程序管理器将不会将SQL_CHAR数据映射到SQL_WCHAR。 Unicode 驱动程序必须接受SQL_CHAR数据。  
  
 驱动程序管理器在 Unicode 中存储驱动程序和 DSN 名称，并根据需要将其映射到 ANSI。 如果 Unicode 字符无法映射到 ANSI 字符（如果驱动程序和 DSN 名称中使用了非计算机本机代码页的代码页的字符，则无法转换的字符由系统提供的默认字符表示。
