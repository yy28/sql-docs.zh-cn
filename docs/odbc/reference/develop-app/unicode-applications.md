---
title: "Unicode 应用程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c99c74a1a294d7d43774fe9d53d169eece98d3ad
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="unicode-applications"></a>Unicode 应用程序
你可以重新编译应用程序作为 Unicode 应用程序在两种方式之一：  
  
-   包括 Unicode **#define**包含在应用程序中的 Sqlucode.h 标头文件。  
  
-   使用编译器的 Unicode 选项将应用程序进行编译。 （此选项将不同的编译器不同。）  
  
 若要将转换为 Unicode 应用程序的 ANSI 应用程序，请编写应用程序存储并将 Unicode 数据传递。 此外，必须将对支持 SQLPOINTER 自变量的函数的调用转换为使用的字节数。  
  
 如果应用程序调用 ODBC API 函数 （不带后缀），作为 Unicode 应用程序，编译应用程序后，驱动程序管理器识别形式 Unicode 应用程序的应用程序，并将转换到 Unicode 函数 （与函数调用*W*后缀) 如果基础的驱动程序支持 Unicode。 当 ANSI 应用程序进行调用不带后缀的函数时，驱动程序管理器将其转换为 ANSI 如果基础的驱动程序支持 ANSI。 如果应用程序和驱动程序支持相同的字符编码，驱动程序管理器将传递到该驱动程序 （带有 ANSI 应用程序特定异常） 通过调用。  
  
 应用程序可以调用这两个 Unicode 函数 (与*W*后缀) 和 ANSI 函数 (带有或不带*A*后缀)。 可以混合 Unicode 和 ANSI 函数调用。 如果要使用的是光标库，但是，不能混合 Unicode 和 ANSI 函数调用。 游标库是 Unicode 或 ANSI，不混合。  
  
 可以编写应用程序，以便它可以编译为 Unicode 应用程序或 ANSI 应用程序。 在这种情况下，字符数据类型可声明为 SQL_C_TCHAR。 这是插入 SQL_C_WCHAR，如果应用程序编译为 Unicode 应用程序，或者插入 SQL_C_CHAR，如果它被编译成 ANSI 应用程序的宏。 因为 length 参数的大小会更改 （对于字符串数据类型） 应用程序程序员必须小心采用 SQLPOINTER 作为其自变量的函数的具体取决于应用程序是否 ANSI 或 Unicode。  
  
 可以在三种方式之一中调用函数： 作为仅限 Unicode 的函数调用 (使用*W*后缀)，为仅限 ANSI 的函数调用 (使用*A*后缀)，或作为无后缀 ODBC 函数调用。 三种形式的函数的自变量是相同的。 只有这些函数与 SQLCHAR\*自变量或指向字符串的 SQLPOINTER 参数需要 Unicode 和 ANSI 窗体。 对于具有可以为字符类型，如声明的自变量的函数**SQLBindCol**或**SQLGetData** （其中没有 Unicode 和 ANSI 窗体），该参数可以声明为 Unicode 类型，ANSI 类型，或者在 C 的情况下的类型自变量，SQL_C_TCHAR 宏。 有关详细信息，请参阅[Unicode 数据](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 应用程序可以编写为 Unicode 应用程序，即使没有 Unicode 驱动程序可用于它以使用。 驱动程序管理器将 Unicode 函数和数据类型映射到 ANSI。 有一些限制为可执行的 ANSI 映射到 Unicode。 Unicode 应用程序以使用 Unicode 驱动程序存在将导致更好的性能，并且将删除 ANSI 映射到 Unicode 中固有的限制。

