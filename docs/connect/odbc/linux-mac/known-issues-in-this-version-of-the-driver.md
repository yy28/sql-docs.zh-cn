---
title: "此版本的驱动程序中的已知问题 |Microsoft 文档"
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
- known issues
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 50f9efe65f14dbd73ccbc3c6e81307c3893c469f
ms.openlocfilehash: 62fd9dd8bf2e11fe39ffaa2e893ded55b214b09c
ms.contentlocale: zh-cn
ms.lasthandoff: 11/08/2017

---
# <a name="known-issues-in-this-version-of-the-driver"></a>此版本驱动程序中的已知问题

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本主题包含有关在 Linux 和 macOS 上的 SQL Server 的 Microsoft ODBC Driver 13 的已知问题列表。

其他问题将在 [Microsoft ODBC 驱动程序团队博客](http://blogs.msdn.com/b/sqlnativeclient/)上发布。  

- Windows、 Linux 和 macOS 请以不同的方式将字符转换从私有使用区 (PUA) 或 End User-Defined 字符 (EUDC)。 中的服务器上执行转换[!INCLUDE[tsql](../../../includes/tsql_md.md)]使用 Windows 转换库。 驱动程序中的转换使用的 Windows、 Linux 或 macOS 转换库。 在执行这些转换时，每个库可能会产生不同的结果。 有关详细信息，请参阅 [最终用户定义的字符和专用区字符](http://msdn.microsoft.com/library/dd317802.aspx)。

- 如果客户端编码为 utf-8，驱动程序管理器不始终正确地转换从 utf-8 为 utf-16。 目前，当 1 时，将发生数据损坏或字符串中的多个字符不是有效的 utf-8 字符。 ASCII 字符将会正确映射。 当调用 SQLCHAR 版本的 ODBC API（例如，SQLDriverConnectA）时，驱动程序管理器将尝试此转换。 当调用 SQLWCHAR 版本的 ODBC API（例如，SQLDriverConnectW）时，驱动程序管理器不会尝试此转换。  

- *Columnsize 类型*参数**SQLBindParameter** SQL 类型中的字符数是指时*BufferLength*是应用程序的中的字节数缓冲区。 但是，如果 SQL 数据类型是`varchar(n)`或`char(n)`、 应用程序将参数绑定为 SQL_C_CHAR 或 SQL_C_VARCHAR，和客户端的字符编码为 utf-8，可能会从驱动程序即使收到"字符串数据，右截断"错误值*columnsize 类型*符合服务器上的数据类型的大小。 由于字符编码之间的转换可能会更改数据的长度，将出现此错误。 例如，右单引号字符 (U + 2019) 中 CP 1252 为单字节 0x92，但在 3 字节序列 0xe2 作为 utf-8 编码 0x80 0x99。

例如，如果你的编码为 utf-8 和为两个指定 1 *BufferLength*和*columnsize 类型*中**SQLBindParameter**为 out 参数，然后尝试检索存储在上述字符`char(1)`列在服务器上 （使用 CP 1252），驱动程序，尝试将其转换为 3 字节 utf-8 编码，但无法容纳结果到 1 个字节的缓冲区。 在另一个方向，它将比较*columnsize 类型*与*BufferLength*中**SQLBindParameter**执行不同的代码页之间的转换操作上之前客户端和服务器。 因为 *ColumnSize* 的值 1 小于 *BufferLength* 的值（例如）3，因此驱动程序将生成一个错误。 若要避免此错误，确保数据的长度后转换在指定的缓冲区或列中发挥作用。 请注意， *columnsize 类型*不能大于 8000`varchar(n)`类型。

## <a name="see-also"></a>另请参阅  
[编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[发行说明](../../../connect/odbc/linux-mac/release-notes.md)  


