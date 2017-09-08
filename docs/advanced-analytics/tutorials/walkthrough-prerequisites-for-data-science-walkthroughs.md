---
title: "为 SQL Server 和 R 数据科学演练先决条件 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9d3a579f023a7e6d9805b934edc3f0e9e5ad5e8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="prerequisites-for-the-data-science-walkthrough-for-sql-server-and-r"></a>为 SQL Server 和 R 数据科学演练的先决条件

我们建议你本演练在便携式计算机或其他计算机上已安装的 Microsoft R 库。 你必须能够连接，在同一网络上为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]机器学习服务并启用的 R 语言的计算机。

你可以同时具有的计算机上运行演练[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 R 开发环境，但我们不建议此配置适用于生产环境。

## <a name="install-machine-learning-for-sql-server"></a>安装 SQL Server 的机器学习

你必须有权对 R 安装，使用以下任一支持的 SQL Server 的实例：

+ SQL server 自 2017 年 1 机器学习服务 （数据库）
+ SQL Server 2016 R Services

有关详细信息，请参阅[设置 SQL Server R Services (数据库中](../r/set-up-sql-server-r-services-in-database.md)。

> [!IMPORTANT]
> 请务必使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或更高版本。 以前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持与 R 集成。但是，可使用旧版的 SQL 数据库作为 ODBC 数据源。

## <a name="install-an-r-development-environment"></a>安装的 R 开发环境

对于本演练，我们建议你使用的 R 开发环境。 下面是一些建议：

- **R Tools for Visual Studio** (RTVS) 是免费的插件，提供 Intellisense、 调试、 以及 Microsoft。 你可将其用于 R Server 和 SQL Server 计算机学习 Services 支持。 若要下载，请参阅 [R Tools for Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)。

- **Microsoft R Client** 是一种轻型开发工具，支持使用 ScaleR 包在 R 中进行开发。 若要了解此工具，请参阅 [Microsoft R 客户端入门](https://msdn.microsoft.com/microsoft-r/r-client-get-started)。

- **RStudio** 是广受欢迎的 R 开发环境之一。 有关详细信息，请参阅 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)。

    无法完成本教程中使用 RStudio 或其他环境中; 的泛型安装你还必须的 Microsoft R Open 安装 R 包和连接库。 有关详细信息，请参阅 [设置数据科学客户端](../r/set-up-a-data-science-client.md)。

- 在安装时，默认情况下还安装基本 R 工具 (R.exe，RTerm.exe，RScripts.exe) [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]。 如果你不希望安装一个 IDE，你可以使用这些工具。

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>获取对 SQL Server 实例和数据库的权限

若要连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要运行脚本并将数据上载，必须具有有效的登录名的数据库服务器上。  可以使用 SQL 登录凭据或集成 Windows 身份验证信息。 询问数据库管理员联系以配置你在其中使用： 数据库中的以下权限的帐户

- 创建数据库、表、函数和存储过程
- 数据写入表
- 运行 R 脚本能力 (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

对于本演练，我们也可以使用的 SQL 登录名**RTestUser**。 通常，我们建议你使用 Windows 集成身份验证，但出于某些演示目的使用的 SQL 登录名是更简单。

## <a name="change-list"></a>更改列表

+ 此示例最初是使用 SQL Server 2016 R Services 进行开发。 但是，Microsoft R 组件中已引入重大更改，2016 SP1。 具体而言， _varsToDrop_和_varsToKeep_参数已不再支持为 SQL Server 数据源。 Therefre，如果你下载的版本在 SP1 之前，在本教程的它将不能再用于 SP1 版本。

+ 经过测试的当前版本中的示例使用 SQL Server 自 2017 年 1 机器学习服务 （RC1 和 RC2） 的预发布版本。 一般情况下，2016 SP1 和自 2017 年之间的无需修改运行应几乎所有步骤。

## <a name="next-lesson"></a>下一课

[准备使用 PowerShell 的数据](/walkthrough-prepare-the-data.md)

