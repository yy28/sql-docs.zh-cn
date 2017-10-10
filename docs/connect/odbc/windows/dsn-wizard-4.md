---
title: "数据源向导屏幕 4 (ODBC Driver for SQL Server) |Microsoft 文档"
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: d3ba6607f717299bdeb60b649a8c6a1838ab0d17
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="data-source-wizard-screen-4"></a>数据源向导屏幕 4

指定要用于 SQL Server 消息的语言，转换过程中，字符集和 SQL Server 的 ODBC 驱动程序是否应使用区域设置。 还可以控制长时间运行查询的日志记录和驱动程序统计信息设置。

## <a name="options"></a>选项

### <a name="change-the-language-of-sql-server-system-messages-to"></a>将 SQL Server 系统消息的语言更改为

每个 SQL Server 实例可以具有多个集的系统消息，使用不同的语言 （例如，英语、 西班牙语、 法语和等等） 的每个组。 如果对具有多组系统消息的服务器定义一个数据源，您可以指定要为系统消息使用哪种语言。 在此列表中，单击该语言。 如果只在 SQL Server 上安装了一种语言，则此选项将不可用。

### <a name="use-strong-encryption-for-data"></a>对数据使用强加密

选中此选项后，将对通过使用此 DSN 建立的连接传输的数据加密。 默认情况下，即使清除此复选框，也将对登录名加密。

### <a name="trust-server-certificate"></a>信任服务器证书

此选项是适用时，才**对数据进行强加密**已启用。 当选中时，服务器的证书将不验证服务器的正确的主机名，以及由受信任的证书颁发机构颁发。 

### <a name="perform-translation-for-character-data"></a>执行字符数据翻译

选中此复选框后，ODBC driver for SQL Server 将通过使用 Unicode 之间的客户端计算机和 SQL Server 发送的 ANSI 字符串转换。 ODBC 驱动程序有时的 SQL Server 代码页和 Unicode 之间转换，客户端计算机上。 这要求 SQL Server 使用的代码页是一个客户端计算机上可用的代码页。

清除此复选框后，当在客户端应用程序和服务器之间发送 ANSI 字符串时，将不会对 ANSI 字符串中的扩展字符进行翻译。 如果客户端计算机使用 ANSI 代码页 (ACP) 不同于 SQL Server 代码页，采用 ANSI 字符字符串的扩展的字符可能被错误解释。 如果客户端计算机使用的 SQL Server 正在使用其 ACP 相同的代码页，正确解释扩展的字符。

### <a name="use-regional-settings-when-outputting-currency-numbers-dates-and-times"></a>在输出货币、数字、日期和时间时使用区域设置

指定驱动程序使用客户端计算机的区域设置对字符输出字符串中的货币、数字、日期和时间进行格式设置。 驱动程序使用通过数据源连接的用户的 Windows 登录帐户的默认区域设置。 请对仅显示数据的应用程序选择此选项，而对处理数据的应用程序则不要选择此选项。

### <a name="save-long-running-queries-to-the-log-file"></a>将长时间运行的查询保存到日志文件

指定驱动程序记录任何查询，所用时间长于**长查询时间**值。 长时间运行的查询将记录到指定文件中。 若要指定日志文件，请在框中，键入完整路径和文件名，或单击**浏览**通过浏览现有文件目录中选择一个日志文件。

### <a name="long-query-time-milliseconds"></a>长查询时间(毫秒)

为长时间运行的查询日志记录指定一个阈值（毫秒）。 将记录任何运行时间超过该毫秒数的查询。

### <a name="log-odbc-driver-statistics-to-the-log-file"></a>将 ODBC 驱动程序统计信息记录到日志文件

指定记录的统计信息。 统计信息将记录到指定的文件中。 若要指定日志文件，请在框中键入完整的路径和文件名称，或单击**浏览**通过浏览现有文件目录中选择一个日志文件。

统计信息日志是一个制表符分隔文件，可以在 Microsoft Excel 或支持制表符分隔文件的任何其他应用程序中进行分析。

### <a name="connect-retry-count"></a>连接重试计数

指定重试连接尝试失败次数。

### <a name="connect-retry-interval-seconds"></a>连接重试间隔 （秒）

指定每次连接重试尝试之间的秒的数。 有关此操作的详细信息和**连接重试计数**选项，请参见[Windows ODBC 驱动程序中的连接弹性](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)。

### <a name="back"></a>返回

单击此按钮以返回到向导的上一页。

### <a name="finish"></a>完成

如果在此屏幕上指定的信息已完成，你可以单击**完成**。 使用此向导的其他屏幕上指定的所有属性创建 DSN 和您有机会测试新创建的 DSN。

## <a name="next-steps"></a>后续步骤

[数据源向导屏幕 3](../../../connect/odbc/windows/dsn-wizard-3.md)

