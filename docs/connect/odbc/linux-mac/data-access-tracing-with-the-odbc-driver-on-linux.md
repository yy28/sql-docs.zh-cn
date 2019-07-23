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
ms.openlocfilehash: 1fa39cd11f70a661de5c284e56f2ccc0f7a5777f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008820"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Linux 和 macOS 上的 ODBC 驱动程序的数据访问跟踪

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

MacOS 和 Linux 上的 unixODBC 驱动程序管理器支持跟踪 ODBC API 调用入口和退出 ODBC 驱动程序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。

若要跟踪应用程序的 ODBC 行为, 请`odbcinst.ini`编辑文件`[ODBC]`的部分, 将值`Trace=Yes`和`TraceFile`设置为要包含跟踪输出的文件的路径; 例如:

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(也可以使用`/dev/stdout`或任何其他设备名称将跟踪输出发送到其中, 而不是保存到永久性文件中。)使用上述设置, 每当应用程序加载 unixODBC 驱动程序管理器时, 它都会将其执行的所有 ODBC API 调用记录到输出文件中。

完成应用程序跟踪后, `Trace=Yes` `odbcinst.ini`从文件中删除以避免跟踪性能损失, 并确保删除任何不必要的跟踪文件。

跟踪适用于使用 `odbcinst.ini` 中的驱动程序的所有应用程序。 如果不跟踪所有应用程序（例如，为避免公开每位用户的敏感信息），可以使用 `ODBCSYSINI` 环境变量为其提供专用 `odbcinst.ini` 的位置，从而跟踪单个应用程序实例。 例如：

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

在这种情况下, 你`Trace=Yes`可以将`[ODBC Driver 13 for SQL Server]`添加到`/home/myappuser/odbcinst.ini`的部分。

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>确定驱动程序要使用的 odbc.ini 文件

Linux 和 macOS ODBC 驱动程序不知道哪个`odbc.ini`正在使用中, 也不知道该`odbc.ini`文件的路径。 但是, 有关正在使用`odbc.ini`的文件的信息, 请参阅 unixODBC 工具`odbc_config`和`odbcinst`和 unixODBC 驱动程序管理器文档。

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

[UnixODBC 文档](http://www.unixodbc.org/doc/UserManual/)介绍用户和系统 dsn 之间的差异。 摘要:

- 用户 Dsn---它们仅适用于特定用户。 用户可以使用、添加、修改和删除自己的用户 Dsn 来连接。 用户 Dsn 存储在用户主目录或其子目录中的文件中。

- 系统 Dsn---系统上的每个用户都可以使用这些 Dsn 进行连接, 但只能由系统管理员添加、修改和删除它们。 如果用户的用户 DSN 与系统 DSN 的名称相同, 则将在该用户的连接中使用该用户 DSN。

## <a name="see-also"></a>另请参阅

- [编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)
