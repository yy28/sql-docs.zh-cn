---
title: "桌面数据库驱动程序的性能问题 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a1bcedc8266132bf617fe35e78d3a73de10f7876
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="desktop-database-driver-performance-issues"></a>桌面数据库驱动程序的性能问题
若要确保与现有 ANSI 应用程序的兼容性，SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR 数据类型作为公开 SQL_CHAR、 SQL_VARCHAR 和 SQL_LONGVARCHAR Microsoft 访问 4.0 或更高版本的数据源。 数据源不会返回宽 CHAR 数据类型，但仍必须将数据发送到 Jet 宽 Char 窗体中。 请务必了解，转换将发生是否 SQL_C_CHAR 参数或结果列被绑定到 SQL_CHAR ANSI 应用程序中的数据类型。  
  
 当 SQL_C_CHAR 类型绑定到类型 LONGVARCHAR 的参数时，此转换可以是尤其是在内存方面效率低下。 由于 Jet 4.0 引擎是找不到流长文本参数数据，UNICODE 转换缓冲区必须分配，SQL_C_CHAR ANSI 缓冲区的大小的两倍。 最有效的机制适用于应用程序执行 UNICODE 转换并将该参数绑定为 SQL_C_WCHAR 类型。 参数标记为数据在执行，但数据提供多个调用 SQLPutData，长文本数据缓冲区时，而增长。 一种方法来避免的增长这开销"将数据"缓冲区是提供一个可选的长度，通过 SQL_DATA_AT_EXEC_LEN(x)，其中*x*是预期的字节长度。 这将初始化到内部 PutData 缓冲区的大小*x*字节。  
  
> [!NOTE]  
>  可以使用完成一种高效的方式插入或更新的长整型数据**SQLBulkOperations()**或**SQLSetPos()**以及将长整型数据设置为 SQL_DATA_AT_EXEC。 （EXEC_LEN 被忽略这种情况下。）数据可以进行流式处理小区块中通过调用**SQLPutData**多次，这将有效地将数据追加到表。  
  
 当使用 Jet 3.5 数据库通过 Microsoft ODBC 桌面数据库驱动程序的应用程序升级到版本 4.0 时，可能发生某些性能下降和增加的工作集大小。 这是因为当版本 3。*x*使用新版本 4.0 驱动程序打开数据库，它将加载 Jet 4.0。 当 Jet 4.0 打开该数据库，看到数据库为 3。*x*版本，它将加载等效于加载 Jet 3.5 引擎也可安装 ISAM 驱动程序。 若要删除对性能和大小的影响，Jet 3。*x*数据库应压缩到 Jet 4.0 格式数据库。 这将消除加载两个 Jet 引擎，并最大程度减少对数据的代码路径。  
  
 此外，Jet 4.0 引擎是 Unicode 引擎。 存储和操作以 Unicode 的所有字符串。 ANSI 应用程序访问 Jet 3 时。*x*通过 Jet 4.0 引擎，数据的数据库转换从 ansi 标准转换为 Unicode，并返回到 ANSI。 如果数据库升级到版本 4.0 格式，将字符串转换为 Unicode，删除一个级别的字符串转换，以及通过只有一个 Jet 引擎将对数据的代码路径降至最低。

