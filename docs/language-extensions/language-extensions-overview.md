---
title: 什么是 SQL Server 语言扩展？
titleSuffix: ''
description: 语言扩展是 SQL Server 的一项功能，用于执行外部代码。 在 SQL Server 2019 中，支持 Java、Python 和 R。 可以使用扩展性框架在外部代码中使用关系数据。
author: dphansen
ms.author: davidph
ms.date: 10/07/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 09d5643b3a39493843adc0ad2da716b7fda1b332
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934902"
---
# <a name="what-is-sql-server-language-extensions"></a>什么是 SQL Server 语言扩展？
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

语言扩展是 SQL Server 的一项功能，用于执行外部代码。 可以使用[扩展性框架](concepts/extensibility-framework.md)在外部代码中使用关系数据。

在 SQL Server 2019 中，支持 Java、Python 和 R。

> [!NOTE]
> 有关在 SQL Server 中执行 Python 或 R 的详细信息，请参阅 [SQL 机器学习服务](../machine-learning/index.yml)文档。 使用 SQL Server 2019 及更高版本，你可以将自定义 Python 和 R 运行时与语言扩展结合使用。 有关详细信息，请参阅 [Python 自定义运行时](../machine-learning/install/custom-runtime-python.md)和 [R 自定义运行时](../machine-learning/install/custom-runtime-r.md)。

## <a name="what-you-can-do-with-language-extensions"></a>使用语言扩展可执行的操作

语言扩展使用扩展性框架来执行外部代码。 代码执行与核心引擎进程隔离，但与 SQL Server 查询执行完全集成。 你可以在数据的源中执行代码，而无需通过网络提取数据。

外部语言通过 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) 定义。 系统存储过程 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 用作执行代码的接口。

语言扩展可提供多种优势：

+ 数据安全性。 使外部语言执行更接近数据源，避免了浪费性的或不安全的数据移动。
+ 速度。 数据库针对基于集的操作进行了优化。 数据库方面的最新创新（如内存中表）可使汇总和聚合快速进行，并且是对数据科学的一种完美补充。
+ 易于部署和集成。 [!INCLUDE [ssNoVersion](../includes/ssnoversion-md.md)] 是许多其他数据管理任务和应用程序的操作中心点。 通过使用数据库中的数据，可以确保语言扩展使用的数据保持最新且一致。

## <a name="next-steps"></a>后续步骤

+ 安装[用于 SQL Server 的 Python 自定义运行时](../machine-learning/install/custom-runtime-python.md)
+ 安装[用于 SQL Server 的 R 自定义运行时](../machine-learning/install/custom-runtime-r.md)
+ 在 [Windows](install/install-sql-server-language-extensions-on-windows.md) 或 [Linux](../linux/sql-server-linux-setup-language-extensions.md) 上安装 SQL Server 语言扩展
+ 安装[用于 Java 的 Microsoft 扩展性 SDK](how-to/extensibility-sdk-java-sql-server.md)
