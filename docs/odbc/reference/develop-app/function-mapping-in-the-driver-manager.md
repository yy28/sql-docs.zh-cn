---
title: 函数映射中驱动程序管理器 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 40dc214fa7f77dfb81c941095ecd71d3d4bf5a36
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762505"
---
# <a name="function-mapping-in-the-driver-manager"></a>驱动程序管理器中的函数映射
驱动程序管理器支持两个入口点用于采用字符串参数的函数。 未修饰的函数 (**SQLDriverConnect**) 是该函数的 ANSI 格式。 使用修饰 Unicode 窗体*W* (**SQLDriverConnectW**。)  
  
 ODBC 头文件还支持使用修饰的函数*A* (**SQLDriverConnectA**) 为了方便混合 ANSI/Unicode 应用程序。 对所做的调用**A**函数是实际调用未修饰的入口点 (**SQLDriverConnect**。)  
  
 如果使用了 _UNICODE 编译应用程序 **#define**，则 ODBC 标头文件将映射未修饰的函数调用 (**SQLDriverConnect**) 到 Unicode 版本 (**SQLDriverConnectW**.)  
  
 驱动程序管理器将驱动程序识别为 Unicode 驱动程序如果**SQLConnectW**驱动程序支持。  
  
 如果该驱动程序是一个 Unicode 驱动程序，驱动程序管理器，如下所示进行函数调用：  
  
-   将不带字符串自变量或参数的函数直接通过传递给驱动程序。  
  
-   将传递 Unicode 函数 (与*W*后缀) 直接通过向驱动程序。  
  
-   将转换的 ANSI 函数 (与*A*后缀) 到 Unicode 函数 (与*W*后缀) 通过将字符串参数转换为 Unicode 字符并将 Unicode 函数传递给驱动程序。  
  
 如果该驱动程序是 ANSI 驱动程序，驱动程序管理器，如下所示进行函数调用：  
  
-   将不带字符串自变量或参数直接通过函数传递给驱动程序。  
  
-   转换 Unicode 函数 (与*W*后缀) 为 ANSI 函数调用并将其传递给驱动程序。  
  
-   ANSI 函数将直接传递到驱动程序。  
  
 驱动程序管理器是支持 Unicode 的内部。 因此，获得最佳性能被通过 Unicode 应用程序使用 Unicode 驱动程序，因为驱动程序管理器只需将 Unicode 函数通过传递给驱动程序。 在 ANSI 应用程序使用 ANSI 驱动程序，驱动程序管理器必须将字符串转换从 ANSI 到 Unicode 时处理某些函数，如**SQLDriverConnect**。 在处理该函数之后, 驱动程序管理器必须然后将 Unicode 字符串转换为 ANSI 函数发送到 ANSI 驱动程序之前。  
  
 应用程序不应修改或驱动程序返回 SQL_STILL_EXECUTING 或 SQL_NEED_DATA 时读取其绑定的参数缓冲区。 驱动程序管理器会保留，直到该驱动程序返回 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 绑定到 ANSI 的缓冲区。 多线程应用程序不应访问另一个线程在其执行的 SQL 语句的任何绑定的参数值。 驱动程序管理器将数据从 Unicode 转换为 ANSI"就地"和另一个线程可能会看到这些缓冲区中的 ANSI 数据时，驱动程序仍在处理 SQL 语句。 将 Unicode 数据绑定到 ANSI 驱动程序的应用程序必须绑定到相同的地址的两个不同的列。
