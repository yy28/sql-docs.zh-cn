---
title: 此版本的 ODBC Driver for SQL Server 中的已知问题 | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3508277502ad7e3eb3b0e7ff048301c8ed1efdd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "68008779"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>此版本驱动程序中的已知问题

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文包含 Linux 和 macOS 上的 Microsoft ODBC Driver for SQL Server 13、13.1 和 17 的已知问题列表。

其他问题将在 [Microsoft ODBC 驱动程序团队博客](https://blogs.msdn.com/b/sqlnativeclient/)上发布。  

- Windows、Linux 和 macOS 可以采用不同方式转换来自专用区 (PUA) 或最终用户定义的字符 (EUDC) 的字符。 在服务器上执行的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 内的转换将使用 Windows 转换库。 驱动程序中的转换使用 Windows、Linux 或 macOS 转换库。 在执行这些转换时，每个库可能会产生不同的结果。 有关详细信息，请参阅[最终用户定义的字符和专用区字符](/windows/desktop/Intl/end-user-defined-characters)。

- 如果客户端采用 UTF-8 编码，驱动程序管理器不会始终将 UTF-8 正确转换为 UTF-16。 目前，当字符串中的一个或多个字符不是有效的 UTF-8 字符时，会发生数据损坏。 ASCII 字符已正确映射。 当调用 SQLCHAR 版本的 ODBC API（例如 SQLDriverConnectA）时，驱动程序管理器尝试此转换。 当调用 SQLWCHAR 版本的 ODBC API（例如，SQLDriverConnectW）时，驱动程序管理器不会尝试此转换。  

- SQLBindParameter 的 ColumnSize 参数指的是 SQL 类型的字符数，而 BufferLength 是应用程序缓冲区中的字节数    。 但是，如果 SQL 数据类型为 `varchar(n)` 或 `char(n)` 且应用程序将参数绑定为 SQL_C_CHAR 或 SQL_C_VARCHAR 并且客户端的字符编码为 UTF-8，可能会从驱动程序收到“字符串数据，右截断”错误，即使 ColumnSize 的值与服务器上的数据类型大小保持一致  。 出现此错误是因为字符编码之间的转换可能会更改数据的长度。 例如，右单引号字符 (U+2019) 以 CP-1252 编码为单字节 0x92，但以 UTF-8 则编码为 3 个字节序列 - 0xe2 0x80 0x99。

例如，如果采用 UTF-8 编码，并且为 out 参数的 SQLBindParameter 中的 BufferLength 和 ColumnSize 均指定 1，然后尝试检索存储在服务器上的  *列中的前一个字符（使用 CP-1252），则驱动程序会尝试将其转换为 3 个字节的 UTF-8 编码，但无法使结果适合 1 个字节的缓冲区*   `char(1)`。 如果条件相反，它会比较 SQLBindParameter 中的 ColumnSize 和 BufferLength，然后在客户端和服务器上的不同代码页之间进行转换    。 因为 *ColumnSize* 的值 1 小于 *BufferLength* 的值（例如）3，因此驱动程序将生成一个错误。 要避免此错误，请确保转换后的数据长度适合指定的缓冲区或列。 请注意，对于  *类型，ColumnSize 不能大于 8000*`varchar(n)`。

## <a name="see-also"></a>另请参阅  
[编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[发行说明](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  

