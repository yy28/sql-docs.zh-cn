---
title: 使用文件数据源进行连接 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c752fc3b09c06c68dcc216cacac63744dc3101b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287407"
---
# <a name="connecting-using-file-data-sources"></a>使用文件数据源连接
文件数据源的连接信息存储在 .dsn 文件中。 因此，连接字符串可以由单个用户重复使用，也可以在多个用户之间共享（如果他们安装了适当的驱动程序）。 该文件包含驱动程序名称（或不可共享文件数据源时的另一个数据源名称），以及可选的连接字符串，该字符串可用于**SQLDriverConnect**。 驱动程序管理器从 .dsn 文件中的关键字构建对**SQLDriverConnect**调用的连接字符串。  
  
 文件数据源允许应用程序指定连接选项，而无需构建用于**SQLDriverConnect**的连接字符串。 文件数据源通常是通过指定**SAVEFILE**关键字创建的，该关键字会导致驱动程序管理器保存由调用**SQLDriverConnect**到 .dsn 文件的输出连接字符串。 可以通过使用**FILEDSN**关键字调用**SQLDriverConnect**来重复使用该连接字符串。 这简化了连接过程，并提供了连接字符串的持久源。  
  
 还可以通过在安装程序 DLL 中调用**SQLCreateDataSource**来创建文件数据源。 信息可以通过调用**SQLWriteFileDSN**写入 .dsn 文件，并通过调用**SQLReadFileDSN**从 .dsn 文件中读取;这两个函数也在安装程序 DLL 中。 有关安装程序 DLL 的信息，请参阅[配置数据源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 用于连接信息的关键字位于 .dsn 文件的 [ODBC] 部分。 可共享 .dsn 文件在 [ODBC] 部分中将具有的最小信息是 DRIVER 关键字：  
  
```  
DRIVER = SQL Server  
```  
  
 可共享的 .dsn 文件通常包含连接字符串，如下所示：  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 当文件数据源不可共享时，.dsn 文件仅包含**DSN**关键字。 当驱动程序管理器在不可共享的文件数据源中发送信息时，它将根据需要连接到**DSN**关键字指示的数据源。 不可共享的 .dsn 文件将包含以下关键字：  
  
```  
DSN = MyDataSource  
```  
  
 用于文件数据源的连接字符串是 .dsn 文件中指定的关键字和调用**SQLDriverConnect**中的连接字符串中指定的关键字的合并。 如果 .dsn 文件中的任何关键字与连接字符串中的关键字冲突，驱动程序管理器将决定应使用哪个关键字值。 有关详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>另请参阅  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
