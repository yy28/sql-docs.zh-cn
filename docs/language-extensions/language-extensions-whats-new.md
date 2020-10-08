---
title: SQL Server 语言扩展中有哪些新增功能？
titleSuffix: ''
description: 了解 SQL Server 语言扩展的新增功能，这些功能扩大、扩展并深化了外部语言与数据平台之间的集成。
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f90d3d25009676f33f57c42ced48284dfae75bd2
ms.sourcegitcommit: 346a37242f889d76cd783f55aeed98023c693610
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91765748"
---
# <a name="whats-new-in-sql-server-language-extensions"></a>SQL Server 语言扩展中有哪些新增功能？
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

随着我们继续扩大、扩展和深化外部语言与数据平台之间的集成，每个版本的 SQL Server 中都将添加[语言扩展](language-extensions-overview.md)功能。 

## <a name="new-in-sql-server-2019"></a>SQL Server 2019 中的新增功能 

此版本添加了对 SQL Server 中语言扩展的支持。 有关此版本中所有功能的详细信息，请参阅 [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)和 [SQL Server 2019 的发行说明](../sql-server/sql-server-version-15-release-notes.md)。

- Windows 和 Linux 上的默认 Java 运行时是 Open Zulu JRE，并且包含在 [Windows 上的 SQL Server 语言扩展安装](install/install-sql-server-language-extensions-on-windows.md)和 [Linux 上的 SQL Server 语言扩展安装](../linux/sql-server-linux-setup-language-extensions.md)中。
- 支持的 [Java 数据类型](how-to/java-to-sql-data-types.md)。
- [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md)，用于在 SQL Server 中注册外部语言（例如 Java）。
- [用于 Java 的 Microsoft 扩展性 SDK](how-to/extensibility-sdk-java-sql-server.md)。
- 在 Windows 和 Linux 上，可以使用 [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) 语句在外部库中访问 Java 代码。 了解详细信息：[如何从 SQL Server 调用 Java](how-to/call-java-from-sql.md)。
- Windows 和 Linux 上的 [Java 语言扩展](language-extensions-overview.md)。 可以通过分配权限并设置路径，使编译后的 Java 代码可用于 SQL Server。 可访问 SQL Server 的客户端应用可以使用数据并通过调用 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 运行代码，这与 SQL Server 机器学习服务上用于 R 和 Python 集成的过程相同。

## <a name="next-steps"></a>后续步骤

+ 在 [Windows](install/install-sql-server-language-extensions-on-windows.md) 或 [Linux](../linux/sql-server-linux-setup-language-extensions.md) 上安装 SQL Server 语言扩展