---
title: 适用于 SQL Server 的已知问题在此版本的驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15c0402f83dec65b6476d481b77553a037d4fa47
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602027"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>此版本驱动程序中的已知问题

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文包含 Microsoft ODBC Driver 13、 13.1 和 17 for SQL Server Linux 和 macOS 上的已知问题的列表。

其他问题将在 [Microsoft ODBC 驱动程序团队博客](https://blogs.msdn.com/b/sqlnativeclient/)上发布。  

- Windows、Linux 和 macOS 可以采用不同方式转换来自专用区 (PUA) 或最终用户定义的字符 (EUDC) 的字符。 在服务器上执行的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 内的转换将使用 Windows 转换库。 驱动程序中的转换使用的 Windows、 Linux 或 macOS 转换库。 在执行这些转换时，每个库可能会产生不同的结果。 有关详细信息，请参阅[最终用户定义的字符和专用区字符](/windows/desktop/Intl/end-user-defined-characters)。

- 如果客户端编码为 utf-8，驱动程序管理器不始终正确转换从 utf-8 到 utf-16。 目前，当字符串中的一个或多个字符不是有效的 utf-8 字符时，会发生数据损坏。 ASCII 字符已正确映射。 当调用 SQLCHAR 版本的 ODBC API（例如 SQLDriverConnectA）时，驱动程序管理器尝试此转换。 当调用 SQLWCHAR 版本的 ODBC API（例如，SQLDriverConnectW）时，驱动程序管理器不会尝试此转换。  

- *ColumnSize*的参数**SQLBindParameter**指的是 SQL 类型中的字符数而*BufferLength*是在应用程序中的字节数缓冲区。 但是，如果 SQL 数据类型为 `varchar(n)` 或 `char(n)` 且应用程序将参数绑定为 SQL_C_CHAR 或 SQL_C_VARCHAR 并且客户端的字符编码为 UTF-8，可能会从驱动程序收到“字符串数据，右截断”错误，即使 ColumnSize 的值与服务器上的数据类型大小保持一致。 因为字符编码之间的转换可能会更改数据的长度，则会发生此错误。 例如，右单引号字符 (U + 2019) 在 CP-1252 单字节 0x92，但在 3 字节序列 0xe2 作为 utf-8 编码 0x80 0x99。

例如，如果你的编码为 utf-8 和两个指定 1 *BufferLength*并*ColumnSize*中**SQLBindParameter**为输出参数，然后尝试到检索存储在前面的字符`char(1)`列在服务器上 （使用 CP-1252年），驱动程序，尝试将其转换为的 3 字节 utf-8 编码，但不适合放 1 字节缓冲区的结果。 在另一个方向，它将进行比较*ColumnSize*与*BufferLength*中**SQLBindParameter**上执行的不同代码页之间的转换前客户端和服务器。 因为 *ColumnSize* 的值 1 小于 *BufferLength* 的值（例如）3，因此驱动程序将生成一个错误。 若要避免此错误，请确保数据的长度后转换适用于指定的缓冲区或列。 请注意， *ColumnSize*不能大于 8000`varchar(n)`类型。

## <a name="see-also"></a>另请参阅  
[编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[发行说明](../../../connect/odbc/linux-mac/release-notes.md)  

