---
title: 驱动程序管理器中的函数映射 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2bfa535d4175c109e96098dd1e40e93be9521de2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069690"
---
# <a name="function-mapping-in-the-driver-manager"></a>驱动程序管理器中的函数映射
对于采用字符串参数的函数，驱动程序管理器支持两个入口点。 未修饰的函数（**SQLDriverConnect**）是函数的 ANSI 形式。 Unicode 形式使用*W* （**SQLDriverConnectW**）修饰。  
  
 ODBC 头文件还支持使用 A （**SQLDriverConnectA**）修饰的函数 *，* 以方便混合 ANSI/Unicode 应用程序。 对**函数进行的调用**实际上会调用未修饰的入口点（**SQLDriverConnect**）。  
  
 如果在 _UNICODE **#define**中编译应用程序，则 ODBC 标头文件会将未修饰的函数调用（**SQLDriverConnect**）映射到 UNICODE 版本（**SQLDriverConnectW**）。  
  
 如果驱动程序支持**SQLConnectW** ，则驱动程序管理器会将驱动程序识别为 Unicode 驱动程序。  
  
 如果驱动程序是 Unicode 驱动程序，则驱动程序管理器将按如下所示进行函数调用：  
  
-   将没有字符串参数或参数的函数直接传递给驱动程序。  
  
-   直接将 Unicode 函数（带有*W*后缀）传递给驱动程序。  
  
-   通过将字符串参数转换为 Unicode 字符并将 Unicode 函数传递给驱动程序，将 ANSI 函数（带有*A*后缀）转换为 unicode 函数（带有*W*后缀）。  
  
 如果驱动程序是 ANSI 驱动程序，则驱动程序管理器将按如下所示进行函数调用：  
  
-   将没有字符串参数或参数的函数直接传递给驱动程序。  
  
-   将 Unicode 函数（带*W*后缀）转换为 ANSI 函数调用，并将其传递给驱动程序。  
  
-   将 ANSI 函数直接传递给驱动程序。  
  
 驱动程序管理器在内部启用了 Unicode。 因此，使用 Unicode 驱动程序的 Unicode 应用程序会获得最佳性能，因为驱动程序管理器只是将 Unicode 函数传递给驱动程序。 当 ANSI 应用程序使用 ANSI 驱动程序时，在处理某些函数（如**SQLDriverConnect**）时，驱动程序管理器必须将字符串从 ANSI 转换为 Unicode。 处理函数之后，驱动程序管理器必须在将该函数发送到 ANSI 驱动程序之前，将该 Unicode 字符串转换回 ANSI。  
  
 当驱动程序返回 SQL_STILL_EXECUTING 或 SQL_NEED_DATA 时，应用程序不应修改或读取其绑定参数缓冲区。 驱动程序管理器使缓冲区绑定到 ANSI，直到驱动程序返回 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO 或 SQL_ERROR。 多线程应用程序不应获得对另一个线程在其上执行 SQL 语句的任何绑定参数值的访问权限。 驱动程序管理器将数据从 Unicode 转换为 ANSI "就地"，另一个线程可能会在这些缓冲区中看到 ANSI 数据，而驱动程序仍在处理 SQL 语句。 将 Unicode 数据绑定到 ANSI 驱动程序的应用程序不能将两个不同的列绑定到同一个地址。
