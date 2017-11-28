---
title: "使用 ODBC 驱动程序在 Linux 和 macOS 上的数据访问跟踪 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4a8c00866759a3cc9732083891e911eea9c2677b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>使用 ODBC 驱动程序在 Linux 和 macOS 上的数据访问跟踪
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

在 macOS 和 Linux 上的 unixODBC 驱动程序管理器支持跟踪 ODBC API 调用入口和退出的 ODBC driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。

若要跟踪你的应用程序的 ODBC 行为，编辑`odbcinst.ini`文件的`[ODBC]`部分设置的值`Trace=Yes`和`TraceFile`为将包含跟踪输出; 的文件的路径例如：

```  
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```  

(你还可以使用`/dev/stdout`或任何其他设备名称发送跟踪输出存在而不是到持久的文件。)使用上面的设置，每次应用程序加载 unixODBC 驱动程序管理器，它会记录到输出文件它执行的 ODBC API 调用。

在完成跟踪你的应用程序后，删除`Trace=Yes`从`odbcinst.ini`文件以避免对性能的跟踪，影响，并确保将删除任何不必要的跟踪文件。
  
跟踪适用于所有使用中的驱动程序的应用程序`odbcinst.ini`。 若要不跟踪所有应用程序 （例如，为避免泄漏敏感的每个用户信息），可以跟踪单个应用程序实例通过提供它的专用位置`odbcinst.ini`，使用`ODBCSYSINI`环境变量。 例如：  
  
```  
$ ODBCSYSINI=/home/myappuser myapp
```  
  
在这种情况下，你可以添加`Trace=Yes`到`[ODBC Driver 13 for SQL Server]`部分`/home/myappuser/odbcinst.ini`。

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>确定驱动程序正在使用哪些 odbc.ini 文件

Linux 和 macOS ODBC 驱动程序不知道哪个`odbc.ini`正被使用或指向的路径`odbc.ini`文件。 但是，了解其中哪些`odbc.ini`文件正在使用的 unixODBC 工具位于`odbc_config`和`odbcinst`，和从 unixODBC 驱动程序管理器文档。  
  
例如，以下命令将打印 （以及其他信息） 的系统和用户的位置`odbc.ini`分别包含系统和用户 Dsn 文件：

```
$ odbcinst -j
unixODBC 2.3.1
DRIVERS............: /etc/odbcinst.ini
SYSTEM DATA SOURCES: /etc/odbc.ini
FILE DATA SOURCES..: /etc/ODBCDataSources
USER DATA SOURCES..: /home/odbcuser/.odbc.ini`
SQLULEN Size.......: 8
SQLLEN Size........: 8
SQLSETPOSIROW Size.: 8
```

[UnixODBC 文档](http://www.unixodbc.org/doc/UserManual/)介绍用户和系统 Dsn 之间的差异。 摘要：  

- 用户 Dsn---这些是仅可供特定用户的 Dsn。 用户可以使用连接、 添加、 修改和删除其自己的用户 Dsn。 用户 Dsn 存储在用户的主目录或其中的子目录中的文件。
  
- 系统 Dsn---这些 Dsn 可用于在系统上每个用户连接使用它们，但可以仅进行添加、 修改和删除系统管理员。 如果用户具有的系统 DSN 与同名的用户 DSN，将通过该用户在连接时使用用户 DSN。

## <a name="see-also"></a>另请参阅
[编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)
