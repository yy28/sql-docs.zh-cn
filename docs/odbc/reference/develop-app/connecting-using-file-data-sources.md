---
title: 使用文件数据源进行连接 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa340c64f6eb92d803d8918bc99ecf112b19f1e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083107"
---
# <a name="connecting-using-file-data-sources"></a>使用文件数据源连接
文件数据源的连接信息存储在 .dsn 文件中。 因此，如果安装了适当的驱动程序，则单个用户或在多个用户之间共享连接字符串即可。 此文件包含驱动程序名称（或者在 unshareable 文件数据源的情况下为其他数据源名称），也可以包含**SQLDriverConnect**使用的连接字符串。 驱动程序管理器通过 .dsn 文件中的关键字，为对**SQLDriverConnect**的调用生成连接字符串。  
  
 文件数据源允许应用程序指定连接选项，而无需生成用于**SQLDriverConnect**的连接字符串。 文件数据源通常是通过指定**SAVEFILE**关键字创建的，这将导致驱动程序管理器将对**SQLDriverConnect**的调用创建的输出连接字符串保存到 .dsn 文件中。 可以通过使用**FILEDSN**关键字调用**SQLDriverConnect**来重复使用此连接字符串。 这可以简化连接过程，并提供连接字符串的持久源。  
  
 还可以通过在安装程序 DLL 中调用**SQLCreateDataSource**来创建文件数据源。 可以通过调用**SQLWriteFileDSN**将信息写入 .dsn 文件，并通过调用**SQLReadFileDSN**读取 .dsn 文件;这两个函数也位于安装程序 DLL 中。 有关安装程序 DLL 的信息，请参阅[配置数据源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 用于连接信息的关键字位于 .dsn 文件的 [ODBC] 部分中。 可共享的 .dsn 文件在 [ODBC] 部分中具有的最小信息是 DRIVER 关键字：  
  
```  
DRIVER = SQL Server  
```  
  
 可共享的 .dsn 文件通常包含一个连接字符串，如下所示：  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 当文件数据源为 unshareable 时，.dsn 文件仅包含**dsn**关键字。 当驱动程序管理器发送 unshareable 文件数据源中的信息时，它会根据需要连接到**DSN**关键字指示的数据源。 Unshareable 文件将包含以下关键字：  
  
```  
DSN = MyDataSource  
```  
  
 用于文件数据源的连接字符串是在**SQLDriverConnect**中调用的在 dsn 文件中指定的关键字和在连接字符串中指定的关键字的联合。 如果 .dsn 文件中的任何关键字与连接字符串中的关键字冲突，则驱动程序管理器会确定应该使用哪个关键字值。 有关详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>另请参阅  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
