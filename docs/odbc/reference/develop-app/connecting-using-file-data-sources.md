---
title: 使用文件数据源连接 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6fec2cea71ba818e955e0b6c2ce31c58f2c07357
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677316"
---
# <a name="connecting-using-file-data-sources"></a>使用文件数据源连接
.Dsn 文件中存储文件数据源的连接信息。 因此，可以重复使用单个用户的或如果他们具有适当的驱动程序安装在多个用户之间共享的连接字符串。 该文件包含驱动程序名称 （或在共享的文件数据源的情况下的另一个数据源名称） 和 （可选） 可以使用一个连接字符串**SQLDriverConnect**。 驱动程序管理器生成连接字符串为调用**SQLDriverConnect**从.dsn 文件中的关键字。  
  
 文件数据源，应用程序可以指定连接选项，而无需生成与一起使用的连接字符串**SQLDriverConnect**。 文件创建数据源通常是通过指定**SAVEFILE**关键字，这会导致驱动程序管理器，以保存通过调用创建的输出连接字符串**SQLDriverConnect** .dsn 文件。 可以通过调用中重复使用连接字符串**SQLDriverConnect**与**FILEDSN**关键字。 这简化了连接过程，并提供的永久源的连接字符串。  
  
 此外可以通过调用创建的文件数据源**SQLCreateDataSource**安装程序 DLL 中。 信息可以通过调用写入到.dsn 文件**SQLWriteFileDSN**，并通过调用从.dsn 文件读取**SQLReadFileDSN**; 这两个函数还将安装程序 DLL。 有关安装程序 DLL 的信息，请参阅[配置数据源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 输入连接信息所使用的关键字是.dsn 文件的 [ODBC] 部分中。 可共享.dsn 文件必须在 [ODBC] 部分中的最少信息是驱动程序关键字：  
  
```  
DRIVER = SQL Server  
```  
  
 可共享.dsn 文件通常包含一个连接字符串，按如下所示：  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 非共享文件数据源时，.dsn 文件仅包含**DSN**关键字。 当驱动程序管理器将信息发送非共享的文件数据源中时，连接到指示的数据源根据需要**DSN**关键字。 非共享.dsn 文件将包含以下关键字：  
  
```  
DSN = MyDataSource  
```  
  
 用于文件数据源的连接字符串是.dsn 文件中指定的关键字和关键字对的调用中的连接字符串中指定的联合**SQLDriverConnect**。 如果任何.dsn 文件中的关键字的连接字符串中的关键字冲突，则驱动程序管理器会决定应使用的关键字值。 有关详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>请参阅  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
