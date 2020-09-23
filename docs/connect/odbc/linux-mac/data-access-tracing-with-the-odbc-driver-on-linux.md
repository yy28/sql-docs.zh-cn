---
title: Linux 和 macOS 上的 ODBC 驱动程序的数据访问跟踪
description: 了解如何在包含 Microsoft ODBC Driver for SQL Server 的 Linux 和 macOS 上启用跟踪，以便在排除应用程序行为故障时输出日志文件。
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69f55104ed73f4d6468de3dcacca54d05cf0ac9a
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288199"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Linux 和 macOS 上的 ODBC 驱动程序的数据访问跟踪

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

macOS 和 Linux 上的 unixODBC 驱动程序管理器支持跟踪 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 ODBC API 调用入口和出口。

若要跟踪应用程序的 ODBC 行为，请编辑 `odbcinst.ini` 文件的 `[ODBC]` 部分，将 `Trace=Yes` 和 `TraceFile` 值设置为要包含跟踪输出的文件的路径，例如：

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

（还可以使用 `/dev/stdout` 或任何其他设备名称将跟踪输出发送到其中，而不是发送到永久性文件中。）使用上述设置，每当应用程序加载 unixODBC 驱动程序管理器时，它都会将其执行的所有 ODBC API 调用记录到输出文件中。

完成应用程序跟踪后，从 `odbcinst.ini` 文件中删除 `Trace=Yes`，这样可以避免跟踪性能下降，同时确保删除了所有不必要的跟踪文件。

跟踪适用于使用 `odbcinst.ini` 中的驱动程序的所有应用程序。 如果不跟踪所有应用程序（例如，为避免公开每位用户的敏感信息），可以使用 `ODBCSYSINI` 环境变量为其提供专用 `odbcinst.ini` 的位置，从而跟踪单个应用程序实例。 例如：

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

在这种情况下，可以将 `Trace=Yes` 添加到 `/home/myappuser/odbcinst.ini` 的 `[ODBC Driver 17 for SQL Server]` 部分。

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>确定驱动程序要使用的 odbc.ini 文件

Linux 和 macOS ODBC 驱动程序不知道正在使用的是哪个 `odbc.ini`，也不知道 `odbc.ini` 文件的路径。 但是，unixODBC 工具 `odbc_config` 和 `odbcinst` 以及 unixODBC 驱动程序管理器文档会提供有关正在使用的 `odbc.ini` 文件的信息。

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

[unixODBC 文档](http://www.unixodbc.org/doc/UserManual/)解释了用户和系统 DSN 之间的差异。 综上所述：

- 用户 DSN - 这些 DSN 仅供特定用户使用。 用户可以添加、修改和删除自己的用户 DSN，并使用它进行连接。 用户 DSN 存储在用户主目录或其子目录中的文件中。

- 系统 DSN - 系统上的每个用户都可以使用这些 DSN 进行连接，但只能由系统管理员执行添加、修改和删除操作。 如果用户的用户 DSN 与系统 DSN 的名称相同，则该用户在连接时将使用用户 DSN。

## <a name="see-also"></a>另请参阅

- [编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)
