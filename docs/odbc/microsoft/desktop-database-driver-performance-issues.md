---
title: 桌面数据库驱动程序性能问题 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 660b7c123d0ddd0a3f1b972fa3b1dc153b15ed50
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071934"
---
# <a name="desktop-database-driver-performance-issues"></a>桌面数据库驱动程序性能问题
为了确保与现有 ANSI 应用程序的兼容性，SQL_WCHAR、SQL_WVARCHAR 和 SQL_WLONGVARCHAR 数据类型公开为 Microsoft Access 4.0 或更高版本的数据源 SQL_CHAR、SQL_VARCHAR 和 SQL_LONGVARCHAR。 数据源不返回宽字符数据类型，但数据仍必须以宽字符形式发送到 Jet。 如果 SQL_C_CHAR 参数或结果列绑定到 ANSI 应用程序中 SQL_CHAR 的数据类型，则必须了解该转换。  
  
 当 SQL_C_CHAR 类型绑定到类型 LONGVARCHAR 的参数时，此转换在内存方面可能会特别低下。 由于 Jet 4.0 引擎无法流式传输 LONGTEXT 参数数据，因此必须分配一个 UNICODE 转换缓冲区，该缓冲区的大小是 SQL_C_CHAR ANSI 缓冲区的两倍。 最有效的机制是让应用程序执行 UNICODE 转换，并将参数绑定为类型 SQL_C_WCHAR。 当某个参数在执行时标记为 "执行中的数据"，并且在多个对 SQLPutData 的调用中提供数据时，将增加 longtext 的数据缓冲区。 避免增加此 "放置数据" 缓冲区开销的一种方法是通过 SQL_DATA_AT_EXEC_LEN （x）提供可选长度，其中*x*是预期的字节长度。 这会将内部 PutData 缓冲区的大小初始化为*x*字节。  
  
> [!NOTE]  
>  可以使用**SQLBulkOperations （）** 或**SQLSetPos （）** 并将长数据设置为 SQL_DATA_AT_EXEC 来完成插入或更新长数据的有效方法。 （在这种情况下，将忽略 EXEC_LEN。）可以通过多次调用**SQLPutData**以区块形式传输数据，这会有效地将数据追加到表。  
  
 当通过 Microsoft ODBC 桌面数据库驱动程序使用 Jet 3.5 数据库的应用程序升级到版本4.0 时，可能会导致性能下降，并且可能会增加工作集大小。 这是因为在版本3上。*x*数据库使用新版4.0 驱动程序打开，它会加载 Jet 4.0。 当 Jet 4.0 打开数据库时，会看到数据库为3。*x*版本，它加载等效于加载 Jet 3.5 引擎的可安装 ISAM 驱动程序。 若要消除性能和大小损失，请执行 Jet 3。*x*数据库应压缩为 Jet 4.0 格式的数据库。 这将避免加载两个 Jet 引擎，并最大限度地减少数据的代码路径。  
  
 此外，Jet 4.0 引擎是一个 Unicode 引擎。 所有字符串都以 Unicode 格式存储和操作。 当 ANSI 应用程序访问 Jet 3 时。*x*数据库通过 Jet 4.0 引擎，将数据从 ANSI 转换为 Unicode 并返回到 ansi。 如果数据库更新为版本4.0 格式，则会将字符串转换为 Unicode，删除一个级别的字符串转换，并通过只经历一个 Jet 引擎来将数据的代码路径降到最低。
