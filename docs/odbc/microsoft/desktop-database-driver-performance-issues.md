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
manager: craigg
ms.openlocfilehash: b4d92d2784649e4366113b3070b54598df585370
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240307"
---
# <a name="desktop-database-driver-performance-issues"></a>桌面数据库驱动程序性能问题
若要确保与现有的 ANSI 应用程序兼容性，SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR 数据类型公开为 SQL_CHAR、 SQL_VARCHAR 和 SQL_LONGVARCHAR 为 Microsoft 访问 4.0 或更高版本的数据源。 数据源不会返回宽字符数据类型，但仍必须将数据发送到 Jet 宽字符形式。 请务必了解是否 SQL_C_CHAR 参数或结果列绑定到 ANSI 应用程序中的 SQL_CHAR 数据类型，转换将需要的位置。  
  
 SQL_C_CHAR 类型绑定到类型 LONGVARCHAR 的参数时，此转换可以是内存占用而言尤其是效率低下。 由于 Jet 4.0 引擎找不到流 LONGTEXT 参数数据，UNICODE 转换缓冲区必须分配的 ANSI SQL_C_CHAR 缓冲区的大小的两倍。 应用程序可以执行 UNICODE 转换并将该参数绑定为 SQL_C_WCHAR 类型是最有效的机制。 当参数标记为执行时数据且数据提供多个调用 SQLPutData 时，一个长文本数据缓冲区就是增长。 一种方法以避免对此不断增长的费用"将数据"缓冲区是提供一个可选的长度，通过 SQL_DATA_AT_EXEC_LEN(x)，其中*x*是预期的字节长度。 这将初始化到的内部 PutData 缓冲区的大小*x*字节。  
  
> [!NOTE]  
>  可使用来完成对插入或更新的长整型数据进行高效**SQLBulkOperations()** 或**SQLSetPos()** 并将长数据设置为 SQL_DATA_AT_EXEC。 （EXEC_LEN 忽略这种情况下。）数据可以流式处理的消息块通过调用**SQLPutData**多次，这将有效地将数据追加到表。  
  
 在使用通过 Microsoft ODBC 桌面数据库驱动程序的 Jet 3.5 数据库的应用程序升级到版本 4.0 中，某些性能下降，增加的工作集大小可能会发生。 这是因为当版本 3。*x*使用新版本 4.0 驱动程序打开数据库，它加载 Jet 4.0。 当 Jet 4.0 打开数据库时，看到数据库为 3。*x*版本，它会加载等效于加载 Jet 3.5 引擎还可安装 ISAM 驱动程序。 若要删除的性能和大小的损失，Jet 3。*x*数据库应压缩到 Jet 4.0 格式数据库。 这将消除加载两个 Jet 引擎并最大程度减少数据的代码路径。  
  
 此外，Jet 4.0 引擎是 Unicode 引擎。 所有字符串是存储和操作以 unicode 格式。 ANSI 应用程序访问 Jet 3 时。*x*通过 Jet 4.0 引擎，数据的数据库转换从 ANSI 到 Unicode，并返回到 ANSI。 如果数据库更新到版本 4.0 格式，字符串将转换为 Unicode，删除一个级别的字符串转换，以及通过只有一个 Jet 引擎将对数据的代码路径降至最低。
