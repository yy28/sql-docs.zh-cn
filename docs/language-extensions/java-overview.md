---
title: 什么是 Java 语言扩展？
description: 在 SQL Server 2019 中，Java、Python 和 R 是受支持的语言扩展。 语言扩展是用于执行外部代码的 SQL Server 功能。  可以使用扩展性框架在外部代码中使用关系数据。
author: cawrites
ms.author: chadam
ms.date: 10/06/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f6b7f2c21aa79ee5c0c9657cf817d9801b5d2891
ms.sourcegitcommit: 2b6760408de3b99193edeccce4b92a2f9ed5bcc6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92175905"
---
# <a name="what-is-java-language-extension"></a>什么是 Java 语言扩展？
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

语言扩展是 SQL Server 的一项功能，用于执行外部代码。 可以使用[扩展性框架](concepts/extensibility-framework.md)在外部代码中使用关系数据。

SQL Server 2019 支持 Java。 默认的 Java 运行时为 Zulu Open JRE。 此外，也可以使用其他 Java JRE 或 SDK。

> [!NOTE]
> 有关在 SQL Server 中执行 Python 或 R 的详细信息，请参阅 [SQL 机器学习服务](../machine-learning/index.yml)文档。 使用 SQL Server 2019 及更高版本，你可以将自定义 Python 和 R 运行时与语言扩展结合使用。 有关详细信息，请参阅 [Python 自定义运行时](../machine-learning/install/custom-runtime-python.md)和 [R 自定义运行时](../machine-learning/install/custom-runtime-r.md)。

## <a name="what-you-can-do-with-language-extensions"></a>使用语言扩展可执行的操作

语言扩展使用扩展性框架来执行外部代码。 代码执行与核心引擎进程隔离，但与 SQL Server 查询执行完全集成。 你可以在数据的源中执行代码，而无需通过网络提取数据。

外部语言通过 [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql) 定义。 系统存储过程 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 用作执行代码的接口。

语言扩展提供了各种优势：

+ 数据安全性。 使外部语言执行更接近数据源，避免了浪费性的或不安全的数据移动。
+ 速度。 数据库针对基于集的操作进行了优化。 数据库方面的最新创新（如内存中表）可使汇总和聚合快速进行，并且是对数据科学的一种完美补充。
+ 易于部署和集成。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 是许多其他数据管理任务和应用程序的操作中心点。 通过使用数据库中的数据，可以确保 Java 使用的数据是一致且最新的。

## <a name="how-to-get-started"></a>如何入门

### <a name="step-1-install-the-software"></a>步骤 1：安装软件

+ [Windows 上的 SQL Server 语言扩展](install/windows-java.md)
+ [Linux 上的 SQL Server 语言扩展](../linux/sql-server-linux-setup-language-extensions-java.md)

### <a name="step-2-configure-a-development-tool"></a>步骤 2：配置开发工具

开发人员通常在自己的笔记本电脑或开发工作站上编写代码。 使用 SQL Server 中的语言扩展，无需更改此流程。 安装完成后，可以在 SQL Server 上运行 Java 代码。

+ 使用喜欢的 IDE 来开发 Java 代码  。

+ 安装 

+ 使用 

+ 使用系统存储过程  。

### <a name="step-3-write-your-first-code"></a>步骤 3：编写第一个代码

从 T-SQL 脚本内执行 Java 代码：

+ [教程：正则表达式与 Java](tutorials/search-for-string-using-regular-expressions-in-java.md)

## <a name="limitations"></a>限制

+ 输入和输出缓冲区中的值数量不得超过 `MAX_INT (2^31-1)`，因为这是 Java 数组中可以分配的最大元素数量。

## <a name="next-steps"></a>后续步骤

+ 安装[用于 SQL Server 的 Python 自定义运行时](../machine-learning/install/custom-runtime-python.md)
+ 安装[用于 SQL Server 的 R 自定义运行时](../machine-learning/install/custom-runtime-r.md)
+ 在 [Windows](../language-extensions/install/windows-java.md) 或 [Linux](../linux/sql-server-linux-setup-language-extensions-java.md) 上安装 SQL Server 语言扩展
+ 安装[用于 Java 的 Microsoft 扩展性 SDK](how-to/extensibility-sdk-java-sql-server.md)
