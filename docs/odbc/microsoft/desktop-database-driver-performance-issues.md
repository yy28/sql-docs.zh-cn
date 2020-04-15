---
title: 桌面数据库驱动程序性能问题 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a819d99a995fd7b287beb66b94f1df526e05f201
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303498"
---
# <a name="desktop-database-driver-performance-issues"></a>桌面数据库驱动程序性能问题
为了确保与现有 ANSI 应用程序的兼容性，SQL_WCHAR、SQL_WVARCHAR 和SQL_WLONGVARCHAR数据类型公开为 Microsoft Access 4.0 或更高数据源SQL_CHAR、SQL_VARCHAR和SQL_LONGVARCHAR。 数据源不返回 WIDE CHAR 数据类型，但数据仍必须以宽字符形式发送到 Jet。 请务必了解，如果SQL_C_CHAR参数或结果列绑定到 ANSI 应用程序中的SQL_CHAR数据类型，则转换将发生。  
  
 当SQL_C_CHAR类型绑定到 LONGVARCHAR 类型的参数时，此转换在内存方面可能特别低效。 由于 Jet 4.0 引擎无法流式传输 LONGTEXT 参数数据，因此必须分配一个 UNICODE 转换缓冲区，该缓冲区的大小是 anSI 缓冲区SQL_C_CHAR两倍。 最有效的机制是应用程序执行 UNICODE 转换并将参数绑定为类型SQL_C_WCHAR。 当参数标记为执行数据，并且数据在 SQLPutData 的多次调用中提供时，将创建一个长文本数据缓冲区。 避免增加此"Put Data"缓冲区的费用的一种方法是通过 SQL_DATA_AT_EXEC_LEN（x）提供可选长度，其中*x*是字节的预期长度。 这将初始化内部 PutData 缓冲区的大小为*x*字节。  
  
> [!NOTE]  
>  可以使用**SQLBulk 操作（）** 或**SQLSetPos（）** 将长数据设置为SQL_DATA_AT_EXEC，实现插入或更新长数据的有效方法。 （在这种情况下，EXEC_LEN将被忽略。数据可以通过多次调用**SQLPutData**以区块进行流式传输，这将有效地将数据追加到表中。  
  
 当通过 Microsoft ODBC 桌面数据库驱动程序使用 Jet 3.5 数据库的应用程序升级到版本 4.0 时，可能会出现一些性能下降和工作集大小的增加。 这是因为当版本 3 时。*x*数据库使用新版本 4.0 驱动程序打开，它加载 Jet 4.0。 当 Jet 4.0 打开数据库，看到数据库为 3 时。*x*版本，它加载一个可安装的ISAM驱动程序，相当于加载Jet 3.5引擎。 要消除性能和尺寸损失，请使用 Jet 3。*x*数据库应压缩到 Jet 4.0 格式数据库中。 这将消除加载两个 Jet 引擎，并最大限度地减少数据的代码路径。  
  
 此外，Jet 4.0 发动机是 Unicode 引擎。 所有字符串都在 Unicode 中存储和操作。 当 ANSI 应用程序访问 Jet 3 时。*x*数据库通过 Jet 4.0 引擎，数据从 ANSI 转换为 Unicode 并返回 ANSI。 如果数据库更新为版本 4.0 格式，字符串将转换为 Unicode，删除一个级别的字符串转换，并通过仅通过一个 Jet 引擎最小化数据的代码路径。
