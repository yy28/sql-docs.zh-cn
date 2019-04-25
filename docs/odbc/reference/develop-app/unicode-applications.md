---
title: Unicode 应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fc9cb98837d206d5279d1f14d4a57ce56782759
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633377"
---
# <a name="unicode-applications"></a>Unicode 应用程序
您可以重新编译为 Unicode 应用程序中有两种应用程序：  
  
-   包括 Unicode **#define**包含在应用程序中 Sqlucode.h 头文件。  
  
-   编译该应用程序使用编译器的 Unicode 选项。 （此选项将为不同的编译器不同。）  
  
 若要将转换到 Unicode 应用程序的 ANSI 应用程序，请编写应用程序存储和传递 Unicode 数据。 此外，必须将对支持 SQLPOINTER 参数的函数的调用转换为使用的字节数。  
  
 应用程序编译为 Unicode 应用程序，如果应用程序调用 ODBC API 函数 （不带后缀） 后，驱动程序管理器识别应用程序作为 Unicode 应用程序，并将转换函数调用到 Unicode 函数 （与*W*后缀) 如果基础驱动程序支持 Unicode。 ANSI 应用程序时会调用不带后缀的函数，驱动程序管理器将其转换为 ANSI 如果基础驱动程序支持 ANSI。 如果应用程序和驱动程序支持相同的字符编码，驱动程序管理器将传递到 （使用 ANSI 应用程序某些例外情况） 驱动程序通过调用。  
  
 应用程序可以调用这两个 Unicode 函数 (与*W*后缀) 和 ANSI 函数 (带有或不带*A*后缀)。 可以混合 Unicode 和 ANSI 函数调用。 如果要使用游标库，但是，不能混合 Unicode 和 ANSI 函数调用。 游标库是 Unicode 或 ANSI，不是混合。  
  
 可以编写一个应用程序，以便它可以编译为 Unicode 应用程序或 ANSI 应用程序。 在这种情况下，字符数据类型可以声明为 SQL_C_TCHAR。 这是一个宏来插入 SQL_C_WCHAR，如果应用程序编译为 Unicode 应用程序，或者插入 SQL_C_CHAR，如果它被编译成 ANSI 应用程序。 因为 length 参数的大小会更改 （适用于字符串数据类型） 应用程序编程人员必须小心的采用 SQLPOINTER 作为其参数，具体取决于应用程序是 ANSI 或 Unicode。  
  
 在三种方式之一来调用函数： 为仅限 Unicode 的函数调用 (与*W*后缀)，与仅限 ANSI 的函数调用 (与*一个*后缀)，或作为无后缀的 ODBC 函数调用。 一个函数的三种形式的参数是相同的。 只有这些函数与 SQLCHAR\*参数或指向字符串的 SQLPOINTER 参数需要 Unicode 和 ANSI 窗体。 有关函数的参数可以声明为字符类型，如**SQLBindCol**或**SQLGetData** （其中没有 Unicode 和 ANSI 窗体），该参数可以声明为 Unicode 类型，ANSI 类型，或在 C 的情况下类型实参，SQL_C_TCHAR 宏。 有关详细信息，请参阅[Unicode 数据](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 应用程序可以编写为 Unicode 应用程序，即使没有 Unicode 驱动程序是可用于以使其使用。 驱动程序管理器将 Unicode 函数和数据类型映射为 ANSI。 没有为 Unicode 到 ANSI 映射可以执行一些限制。 Unicode 应用程序以使用 Unicode 驱动程序存在将导致更好的性能，并将删除的 Unicode 到 ANSI 的映射中固有的限制。
