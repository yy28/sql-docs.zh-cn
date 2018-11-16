---
title: Linux 和 macOS 上的 ODBC 驱动程序的数据访问跟踪 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5cd3795f57f544d5f7003f7aab60be2a08a64229
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607187"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Linux 和 macOS 上的 ODBC 驱动程序的数据访问跟踪
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

UnixODBC 驱动程序管理器在 macOS 和 Linux 上的支持跟踪 ODBC API 调用入口和退出的 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。

若要跟踪应用程序的 ODBC 行为，请编辑`odbcinst.ini`文件的`[ODBC]`部分设置的值`Trace=Yes`和`TraceFile`为的文件将包含在跟踪输出; 该文件夹的路径为例：

```  
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```  

(您还可以使用`/dev/stdout`或任何其他设备名称将发送跟踪输出那里而不是持久的文件。)使用以上设置中，每次应用程序加载 unixODBC 驱动程序管理器中，它将记录到输出文件它执行的 ODBC API 调用。

完成应用程序跟踪后，删除`Trace=Yes`从`odbcinst.ini`文件以避免跟踪会损失性能，并确保任何不必要的跟踪文件将被删除。
  
跟踪适用于使用 `odbcinst.ini` 中的驱动程序的所有应用程序。 如果不跟踪所有应用程序（例如，为避免公开每位用户的敏感信息），可以使用 `ODBCSYSINI` 环境变量为其提供专用 `odbcinst.ini` 的位置，从而跟踪单个应用程序实例。 例如：  
  
```  
$ ODBCSYSINI=/home/myappuser myapp
```  
  
在这种情况下，可以添加`Trace=Yes`到`[ODBC Driver 13 for SQL Server]`一部分`/home/myappuser/odbcinst.ini`。

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>确定驱动程序要使用的 odbc.ini 文件

Linux 和 macOS ODBC 驱动程序不知道在哪个`odbc.ini`正被使用或指向的路径`odbc.ini`文件。 但是，了解其中哪些`odbc.ini`文件位于已从 unixODBC 工具可用`odbc_config`和`odbcinst`，unixodbc 驱动程序管理器文档。  
  
例如，以下命令会打印（其他信息中）可能分别包含系统和用户 DSN 的系统位置和用户 `odbc.ini` 文件：

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

[UnixODBC 文档](https://www.unixodbc.org/doc/UserManual/)阐述用户和系统 Dsn 的区别。 在摘要：  

- 用户 Dsn---这些是仅可供特定用户的 Dsn。 用户可以使用连接、 添加、 修改和删除其自己的用户 Dsn。 用户 Dsn 存储在用户的主目录或其中一个子目录中的文件。
  
- 系统 Dsn---这些 Dsn 可用于在系统上的每个用户使用它们，进行连接，但只能添加、 修改和删除由系统管理员。 如果用户具有相同的系统 DSN 的名称的用户 DSN，将由该用户在连接时使用用户 DSN。

## <a name="see-also"></a>另请参阅
[编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)
