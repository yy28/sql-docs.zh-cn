---
title: 函数映射中驱动程序管理器 |Microsoft 文档
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
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee2e5d3e770ddd605618f6a71161f410dab7ab52
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="function-mapping-in-the-driver-manager"></a>函数映射中驱动程序管理器
驱动程序管理器支持用于采用字符串自变量的函数的两个入口点。 未修饰的函数 (**SQLDriverConnect**) 是函数的 ANSI 格式。 Unicode 窗体用修饰*W* (**SQLDriverConnectW**。)  
  
 ODBC 标头文件还支持使用修饰函数*A，* (**SQLDriverConnectA**) 的混合 ANSI/Unicode 应用程序的便利性。 对所做的调用**A**函数是实际的未修饰的入口点的调用 (**SQLDriverConnect**。)  
  
 如果使用了 _UNICODE 编译应用程序 **#define**，ODBC 标头文件将映射未修饰的函数调用 (**SQLDriverConnect**) 到的 Unicode 版本 (**SQLDriverConnectW**.)  
  
 驱动程序管理器： 将驱动程序识别为 Unicode 驱动程序，如果**SQLConnectW**由驱动程序支持。  
  
 如果 Unicode 驱动程序的驱动程序，则驱动程序管理器调用函数，如下所示：  
  
-   将没有字符串自变量或参数的函数直接通过传递给该驱动程序。  
  
-   将传递 Unicode 函数 (与*W*后缀) 直接通过与驱动程序。  
  
-   将转换 ANSI 函数 (与*A*后缀) 到 Unicode 函数 (与*W*后缀) 通过将字符串自变量转换为 Unicode 字符并将 Unicode 函数传递给该驱动程序。  
  
 如果 ANSI 驱动程序的驱动程序，则驱动程序管理器调用函数，如下所示：  
  
-   将功能，而不必字符串自变量或参数直接通过传递给该驱动程序。  
  
-   将转换 Unicode 函数 (与*W*后缀) 为 ANSI 函数调用并将其传递到该驱动程序。  
  
-   ANSI 函数将直接传递到该驱动程序。  
  
 驱动程序管理器是已启用 Unicode 的内部。 因此，最佳的性能被获取的 Unicode 应用程序使用 Unicode 驱动程序，因为驱动程序管理器只是将 Unicode 函数，通过传递到驱动程序。 在 ANSI 应用程序使用 ANSI 驱动程序，驱动程序管理器必须将字符串转换从 ansi 标准转换为 Unicode 时处理某些函数中，如**SQLDriverConnect**。 在处理该函数之后, 驱动程序管理器必须然后将 Unicode 字符串转换为 ANSI 向 ANSI 驱动程序发送函数之前。  
  
 应用程序不应修改或读取及其绑定的参数缓冲区，该驱动程序返回 SQL_STILL_EXECUTING 或 SQL_NEED_DATA 时。 驱动程序管理器使绑定到 ANSI，直到该驱动程序返回 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 的缓冲区。 多线程应用程序不应访问另一个线程在其执行 SQL 语句的任何绑定的参数值。 驱动程序管理器将数据从 Unicode 转换为 ANSI"就地"和另一个线程可能会看到这些缓冲区中的 ANSI 数据，而该驱动程序仍在处理 SQL 语句。 将 Unicode 数据绑定到 ANSI 驱动程序的应用程序必须绑定到相同的地址的两个不同的列。
