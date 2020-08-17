---
description: Unicode 数据
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f217e6b629936cc835d134c89d972bb1408b9d0b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339113"
---
# <a name="unicode-data"></a>Unicode 数据
提供了 SQL Unicode 数据类型，用于描述本机上以 Unicode 格式保存的数据。 提供 C Unicode 数据类型，使应用程序可以将数据绑定到 Unicode 缓冲区。 驱动程序管理器可以将 Unicode C 类型中的数据转换 (SQL_C_WCHAR) ，使其与 ANSI 驱动程序一起工作。  
  
 ODBC 3.0 或2。*x* 应用程序将始终绑定到 ANSI 数据类型。 为了获得最佳性能，如果 sql 列类型为 ANSI，ODBC 3.5 (或更高) 版本的应用程序应绑定到 ANSI data C 类型，如果 SQL 列类型是 Unicode，则应该绑定到 Unicode C 数据类型。  
  
 SQL Unicode 类型指示器是 SQL_WCHAR、SQL_WVARCHAR 和 SQL_WLONGVARCHAR。 SQL_WCHAR 数据具有固定字符串长度，而 SQL_WVARCHAR 的可变长度为已声明的最大值，SQL_WLONGVARCHAR 的长度可变，且最大值取决于数据源。  
  
 C Unicode 类型指示器 SQL_C_WCHAR。 这是每个 SQL Unicode 类型指示器的默认值。 所有 SQL 类型都可以转换为 SQL_C_WCHAR，SQL_C_WCHAR 可转换为所有 SQL 类型。 应用程序可以通过以下三种方式之一来检索数据：  
  
-   检索 SQL_C_CHAR 数据。  
  
-   检索 SQL_C_WCHAR 数据。  
  
-   将数据声明为 SQL_C_TCHAR。 这是一个宏，如果将应用程序编译为 Unicode 应用程序 SQL_C_CHAR 或将其编译为 ANSI 应用程序，则插入 SQL_C_WCHAR。  
  
 在函数中声明 SQL_C_TCHAR，如下所示：  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 当应用程序编译为 Unicode 应用程序时， *ValueType* 参数将从 SQL_C_TCHAR 更改为 SQL_C_WCHAR。 当应用程序编译为 ANSI 应用程序时， *ValueType* 参数将更改为 SQL_C_CHAR。  
  
 Unicode 驱动程序必须仍支持 ANSI 数据类型，包括 SQL_CHAR。 如果使用 Unicode 驱动程序的应用程序绑定到 SQL_CHAR，则驱动程序管理器不会将 SQL_CHAR 数据映射到 SQL_WCHAR。 Unicode 驱动程序必须接受 SQL_CHAR 的数据。  
  
 驱动程序管理器将驱动程序和 DSN 名称按 Unicode 存储，并根据需要将它们映射到 ANSI。 如果 Unicode 字符不能映射到 ANSI 字符 (如在驱动) 程序中使用的代码页中的字符不是计算机的本机代码页，也不能进行转换，则无法转换的字符由系统提供的默认字符表示。
