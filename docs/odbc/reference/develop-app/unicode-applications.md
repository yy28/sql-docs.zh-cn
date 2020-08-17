---
description: Unicode 应用程序
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee2db77c569876b008d21149c500aa0f1f009b7a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339153"
---
# <a name="unicode-applications"></a>Unicode 应用程序
可以通过以下两种方式之一将应用程序重新编译为 Unicode 应用程序：  
  
-   在应用程序中包括 Sqlucode.h 标头文件中包含的 Unicode **#define** 。  
  
-   用编译器的 Unicode 选项编译应用程序。  (对于不同的编译器，此选项将有所不同。 )   
  
 若要将 ANSI 应用程序转换为 Unicode 应用程序，请编写用于存储和传递 Unicode 数据的应用程序。 此外，必须将对支持 SQLPOINTER 参数的函数的调用转换为使用字节数。  
  
 在将应用程序编译为 Unicode 应用程序后，如果应用程序调用 ODBC API 函数 (没有后缀) ，则驱动程序管理器会将该应用程序识别为 Unicode 应用程序，并将函数调用转换为带有 *W*) 后缀的 unicode 函数 (如果基础驱动程序支持 Unicode，则为。 当 ANSI 应用程序进行不带后缀的函数调用时，如果基础驱动程序支持 ANSI，则驱动程序管理器会将其转换为 ANSI。 如果应用程序和驱动程序都支持相同的字符编码，则驱动程序管理器会将对的调用传递给驱动程序 (，并) ANSI 应用程序的某些异常。  
  
 应用程序可以调用 (带有 *W* 后缀) 和 ANSI 函数的 Unicode 函数， (带有或不带 *后缀) * 。 Unicode 和 ANSI 函数调用可以混合。 但是，如果要使用游标库，则不能混合 Unicode 和 ANSI 函数调用。 游标库为 Unicode 或 ANSI，而不是混合。  
  
 可以编写应用程序，以便可以将其编译为 Unicode 应用程序或 ANSI 应用程序。 在这种情况下，可以将字符数据类型声明为 SQL_C_TCHAR。 这是一个宏，如果将应用程序编译为 Unicode 应用程序 SQL_C_CHAR 或将其编译为 ANSI 应用程序，则插入 SQL_C_WCHAR。 应用程序编程人员必须小心采用 SQLPOINTER 作为其参数的函数，因为长度参数的大小将更改字符串数据类型 () 具体取决于应用程序是 ANSI 还是 Unicode。  
  
 可以通过以下三种方式之一调用函数：作为仅限 Unicode 的函数调用 (带有 *W* 后缀) ，作为仅限 ANSI 的函数调用 (*带有后缀) * ，或作为不带后缀的 ODBC 函数调用。 这三种形式的函数的参数是相同的。 仅具有 SQLCHAR \* 参数的函数或指向字符串的 SQLPOINTER 参数需要 Unicode 和 ANSI 形式。 对于包含可声明为字符类型的参数的函数（例如 **SQLBindCol** 或未) UNICODE 和 ANSI 窗体的 **SQLGetData** (），可以将参数声明为 unicode 类型、ANSI 类型，或者在 C 类型参数的情况下，SQL_C_TCHAR 宏。 有关详细信息，请参阅 [Unicode 数据](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 即使没有 Unicode 驱动程序可供使用，也可以将应用程序编写为 Unicode 应用程序。 驱动程序管理器会将 Unicode 函数和数据类型映射到 ANSI。 对于可以执行的 Unicode 到 ANSI 映射，存在一些限制。 要使用 unicode 应用程序的 Unicode 驱动程序是否存在将导致更好的性能，并删除 Unicode 到 ANSI 映射中固有的限制。
