---
title: RevoScaleR 函数深入探讨教程-SQL Server 机器学习
description: 在本教程中, 了解如何使用 SQL Server 机器学习 R 集成调用 RevoScaleR 函数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c326d51e9b3ac4edac61f97bf5f7fa3143d8d350
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470623"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>教程：将 RevoScaleR R 函数与 SQL Server 数据结合使用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)是一个 Microsoft R 包, 为数据科学和机器学习工作负荷提供分布式并行处理。 对于 SQL Server 中的 R 开发, **RevoScaleR**是一个核心内置包, 其中包含用于创建数据源对象的函数、设置计算上下文、管理包, 并且最重要的是: 从导入到的数据端到端可视化和分析。 SQL Server 中的机器学习算法依赖于**RevoScaleR**数据源。 考虑到**RevoScaleR**的重要性, 知道何时以及如何调用其函数是一种至关重要的技能。 

本教程分为多个部分, 介绍了一系列用于与数据科学相关任务的**RevoScaleR**函数。 在此过程中, 您将了解如何创建远程计算上下文、在本地和远程计算上下文之间移动数据以及在远程 SQL Server 上执行 R 代码。 你还将了解如何在本地和远程服务器上分析和绘制数据, 以及如何创建和部署模型。

## <a name="prerequisites"></a>系统必备

+ [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)r 功能, 或[SQL Server 2016 r Services (数据库内)](../install/sql-r-services-windows-install.md)
  
+ [数据库权限](../security/user-permission.md)和 SQL Server 数据库用户登录

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ IDE (如 RStudio) 或 R 附带的内置 RGUI.EXE 工具

若要在本地和远程计算上下文之间来回切换, 需要两个系统。 本地通常是一种开发工作站, 充分强大的数据科学工作负荷。 在这种情况下, 远程在启用 R 功能 SQL Server 2017 或 SQL Server 2016。 

切换计算上下文的依据是在本地和远程系统上都具有相同版本的**RevoScaleR** 。 在本地工作站上, 你可以通过安装 Microsoft R Client 来获取**RevoScaleR**包和相关的提供程序。

如果需要将客户端和服务器放在同一台计算机上, 请确保安装另一组 Microsoft R 库, 以便从 "远程" 客户端发送 R 脚本。 不要使用在 SQL Server 实例的 program 文件中安装的 R 库。 具体而言, 如果你使用一台计算机, 则需要在这两个位置都使用**RevoScaleR**库来支持客户端和服务器操作。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

有关客户端配置的说明, 请参阅[设置用于 R 开发的数据科学客户端](../r/set-up-a-data-science-client.md)。


## <a name="r-development-tools"></a>R 开发工具

R 开发人员通常使用 Ide 来编写和调试 R 代码。 一些建议如下：

- **针对 Visual Studio 的 R 工具**(RTVS) 是一个免费插件, 为 Microsoft R 提供 Intellisense、调试和支持。可以将其与 R Server 和 SQL Server 机器学习服务一起使用。 若要下载，请参阅 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)。

- **RStudio** 是广受欢迎的 R 开发环境之一。 有关详细信息, 请[https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)参阅。

- 默认情况下, 在 SQL Server 或 R Client 中安装 R 时, 也会安装基本的 R 工具 (Rterm.exe、Rscripts.exe)。 如果不想安装 IDE, 可以使用内置 R 工具来执行本教程中的代码。

请记住, 本地计算机和远程计算机上都需要**RevoScaleR** 。 不能使用 RStudio 的通用安装或缺少 Microsoft R 库的其他环境完成本教程。 有关详细信息，请参阅 [设置数据科学客户端](../r/set-up-a-data-science-client.md)。

## <a name="summary-of-tasks"></a>任务摘要

+ 数据最初是从 CSV 文件或 XDF 文件中获取的。 您可以使用**RevoScaleR**包[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的函数将数据导入到中。
+ 模型定型和评分是使用计算上下文[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]来执行的。 
+ 使用**RevoScaleR**函数来创建新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表, 以保存评分结果。
+ 在服务器上和本地计算上下文中创建绘图。
+ 针对数据库中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的数据定型模型, 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中运行 R。
+ 提取一部分数据, 并将其保存为 XDF 文件, 以便在本地工作站上的分析中重复使用。
+ 通过打开到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库的 ODBC 连接获取用于评分的新数据。 评分是在本地工作站上完成的。
+ 创建一个自定义 R 函数并在服务器计算上下文中运行它以执行模拟。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [第 1 课：创建数据库和权限](deepdive-work-with-sql-server-data-using-r.md)