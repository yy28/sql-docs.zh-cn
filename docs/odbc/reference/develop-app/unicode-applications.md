---
title: 单代码应用程序 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94bd5211c878904453624adb2acd0fe435ebc812
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298943"
---
# <a name="unicode-applications"></a>Unicode 应用程序
您可以通过两种方式之一将应用程序重新编译为 Unicode 应用程序：  
  
-   在应用程序中包括 Sqlucode.h 标头文件中中包含的 Unicode **#define。**  
  
-   使用编译器的 Unicode 选项编译应用程序。 （对于不同的编译器，此选项会有所不同。  
  
 要将 ANSI 应用程序转换为 Unicode 应用程序，请编写应用程序以存储和传递 Unicode 数据。 此外，对支持 SQLPOINTER 参数的函数的调用必须转换为字节的使用计数。  
  
 将应用程序编译为 Unicode 应用程序后，如果应用程序调用 ODBC API 函数（没有后缀），驱动程序管理器将应用程序识别为 Unicode 应用程序，如果基础驱动程序支持 Unicode，则将函数调用转换为 Unicode 函数（带*W*后缀）。 当 ANSI 应用程序在没有后缀的情况下进行函数调用时，如果基础驱动程序支持 ANSI，驱动程序管理器会将其转换为 ANSI。 如果应用程序和驱动程序都支持相同的字符编码，驱动程序管理器会将调用传递到驱动程序（ANSI 应用程序的某些例外情况除外）。  
  
 应用程序可以同时调用 Unicode 函数（带*W*后缀）和 ANSI 函数（带或没有*A*后缀）。 Unicode 和 ANSI 函数调用可以混合。 但是，如果要使用游标库，则不能混合 Unicode 和 ANSI 函数调用。 游标库是 Unicode 或 ANSI，而不是混合体。  
  
 可以编写应用程序，以便它可以编译为 Unicode 应用程序或 ANSI 应用程序。 在这种情况下，字符数据类型可以声明为SQL_C_TCHAR。 这是一个宏，用于插入SQL_C_WCHAR如果应用程序编译为 Unicode 应用程序，或者SQL_C_CHAR（如果应用程序编译为 ANSI 应用程序）插入。 应用程序程序员必须小心以 SQLPOINTER 作为参数的函数，因为长度参数的大小将更改（对于字符串数据类型），具体取决于应用程序是 ANSI 还是 Unicode。  
  
 函数可以通过以下三种方式之一调用：作为仅 Unicode 函数调用（带有*W*后缀）、仅 ANSI 函数调用（带*A*后缀）或作为没有后缀的 ODBC 函数调用。 函数的三种形式的参数是相同的。 只有具有 SQLCHAR\*参数或指向字符串的 SQLPOINTER 参数的函数才需要 Unicode 和 ANSI 窗体。 对于具有可声明为字符类型的参数的函数（如**SQLBindCol**或**SQLGetData（** 没有 Unicode 和 ANSI 窗体），可以将参数声明为 Unicode 类型、ANSI 类型，或者对于 C 类型参数（SQL_C_TCHAR宏）。 有关详细信息，请参阅[Unicode 数据](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 即使没有 Unicode 驱动程序可供它使用，也可以将应用程序编写为 Unicode 应用程序。 驱动程序管理器将 Unicode 函数和数据类型映射到 ANSI。 可以对 UNIcode 到 ANSI 映射进行一些限制。 Unicode 应用程序使用 Unicode 驱动程序将提供更好的性能，并将消除 Unicode 到 ANSI 映射中固有的限制。
