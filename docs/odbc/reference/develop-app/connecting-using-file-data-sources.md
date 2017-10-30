---
title: "使用文件数据源连接 |Microsoft 文档"
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
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5f8a5d949127e7ad87866a0272fbd285fe12ceed
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-using-file-data-sources"></a>使用文件数据源连接
.Dsn 文件中存储文件数据源的连接信息。 因此，可以重复使用单个用户或如果他们具有适当的驱动程序安装在多个用户之间共享的连接字符串。 该文件包含驱动程序名称 （或对于非共享的文件数据源的另一个数据源名称） 和 （可选） 可以使用的连接字符串**SQLDriverConnect**。 驱动程序管理器生成连接字符串，调用**SQLDriverConnect**从.dsn 文件中的关键字。  
  
 文件数据源允许应用程序而无需生成与一起使用的连接字符串中指定连接选项**SQLDriverConnect**。 文件数据源通常创建通过指定**SAVEFILE**关键字，这会导致要保存通过调用创建的输出连接字符串的驱动程序管理器**SQLDriverConnect** .dsn 文件。 可以通过调用中重复使用连接字符串**SQLDriverConnect**与**FILEDSN**关键字。 这简化了连接过程，并提供持久性源的连接字符串。  
  
 此外可以通过调用创建文件数据源**SQLCreateDataSource**在安装程序 DLL。 信息可以通过调用写到.dsn 文件**SQLWriteFileDSN**，并通过调用从.dsn 文件读取**SQLReadFileDSN**; 这些函数都还在安装程序 DLL。 有关安装程序 DLL 的信息，请参阅[配置数据源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 .Dsn 文件的 [ODBC] 部分中的连接信息所使用的关键字。 可共享.dsn 文件应该 [ODBC] 部分中的最少信息是驱动程序关键字：  
  
```  
DRIVER = SQL Server  
```  
  
 可共享.dsn 文件通常包含连接字符串，如下所示：  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 .Dsn 文件共享文件数据源时，仅包含**DSN**关键字。 当驱动程序管理器将信息发送非共享的文件数据源中时，连接到数据源由根据需要**DSN**关键字。 非共享.dsn 文件将包含以下关键字：  
  
```  
DSN = MyDataSource  
```  
  
 用于文件数据源的连接字符串是.dsn 文件中指定的关键字和关键字的调用中的连接字符串中指定的联合**SQLDriverConnect**。 如果任何.dsn 文件中的关键字与连接字符串中的关键字冲突，驱动程序管理器将决定应使用的关键字值。 有关详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>另请参阅  
 [http://support.microsoft.com/kb/165866](http://support.microsoft.com/kb/165866)

