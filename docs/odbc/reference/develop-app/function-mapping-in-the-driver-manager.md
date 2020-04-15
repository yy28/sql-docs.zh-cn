---
title: 驱动程序管理器中的功能映射 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db8e525bb7e8f3e167deb8061a4dd5b75073933c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305578"
---
# <a name="function-mapping-in-the-driver-manager"></a>驱动程序管理器中的函数映射
驱动程序管理器支持具有字符串参数的函数的两个入口点。 未修饰函数 （**SQLDriverConnect**） 是函数的 ANSI 形式. Unicode 窗体用**W（SQLDriverConnectW**）装饰。 *W*  
  
 ODBC 头文件还支持使用*A（* **SQLDriverConnectA**） 修饰的功能，以方便混合 ANSI/Unicode 应用程序。 对**A**函数进行的调用实际上是对未修饰的入口点 **（SQLDriverConnect**）的调用。  
  
 如果应用程序使用 **_UNICODE#define**编译，则 ODBC 标头文件将未修饰的函数调用 **（SQLDriverConnect）** 映射到 Unicode 版本 **（SQLDriverConnectW**）.  
  
 如果驱动程序支持**SQLConnectW，** 驱动程序管理器会将驱动程序识别为 Unicode 驱动程序。  
  
 如果驱动程序是 Unicode 驱动程序，驱动程序管理器会按照如下方式进行函数调用：  
  
-   将没有字符串参数或参数的函数直接传递给驱动程序。  
  
-   将 Unicode 函数（带*W*后缀）直接传递到驱动程序。  
  
-   通过将字符串参数转换为 Unicode 字符并将 Unicode 函数传递给驱动程序，将 ANSI 函数（带*A*后缀）转换为 Unicode 函数（带*W*后缀）。  
  
 如果驱动程序是 ANSI 驱动程序，则驱动程序管理器进行函数调用，如下所示：  
  
-   将没有字符串参数或参数的函数直接传递给驱动程序。  
  
-   将 Unicode 函数（带*W*后缀）转换为 ANSI 函数调用，并将其传递给驱动程序。  
  
-   将 ANSI 函数直接传递给驱动程序。  
  
 驱动程序管理器在内部启用 Unicode。 因此，使用 Unicode 驱动程序的 Unicode 应用程序获得了最佳性能，因为驱动程序管理器只需将 Unicode 函数传递给驱动程序即可。 当 ANSI 应用程序使用 ANSI 驱动程序时，驱动程序管理器在处理某些函数（如**SQLDriverConnect**）时，必须将字符串从 ANSI 转换为 Unicode。 处理函数后，驱动程序管理器必须将 Unicode 字符串转换回 ANSI，然后再将函数发送到 ANSI 驱动程序。  
  
 当驱动程序返回SQL_STILL_EXECUTING或SQL_NEED_DATA时，应用程序不应修改或读取其绑定参数缓冲区。 驱动程序管理器将缓冲区绑定到 ANSI，直到驱动程序返回SQL_SUCCESS、SQL_SUCCESS_WITH_INFO或SQL_ERROR。 多线程应用程序不应访问另一个线程正在执行 SQL 语句的任何绑定参数值。 驱动程序管理器将数据从 Unicode 转换为 ANSI"就位"，另一个线程可能会在这些缓冲区中看到 ANSI 数据，而驱动程序仍在处理 SQL 语句。 将 Unicode 数据绑定到 ANSI 驱动程序的应用程序不得将两个不同的列绑定到同一地址。
