---
title: RevoScaleR 函数深入教程的 SQL Server 机器学习
description: 在本教程中，了解如何调用 RevoScaleR 函数使用 SQL Server 机器学习 R 集成。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 48d65bfe54890c5ea0d8bfdca9c76fa0978a917d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641302"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>教程：SQL Server 数据使用 RevoScaleR R 函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)是一种提供分布式的 Microsoft R 包和并行处理对数据科学和机器学习工作负荷。 SQL Server 中的 R 开发**RevoScaleR**是核心的一个内置的软件包，使用函数来创建数据源对象，设置计算上下文，管理包，最重要的是： 使用数据端到端，从导入到可视化和分析。 SQL Server 中的机器学习算法具有依赖关系**RevoScaleR**数据源。 考虑到的重要性**RevoScaleR**、 了解何时以及如何调用其函数是一项基本技能。 

在此多部分教程中，为您介绍了一系列**RevoScaleR**用于与数据科学任务的函数。 在过程中，您将了解如何创建远程计算上下文，本地和远程计算上下文之间移动数据和远程 SQL Server 上执行 R 代码。 你还了解如何分析和本地和远程服务器上绘制数据以及如何创建和部署模型。

## <a name="prerequisites"></a>先决条件

+ [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)与 R 功能或[SQL Server 2016 R Services （数据库内）](../install/sql-r-services-windows-install.md)
  
+ [数据库权限](../security/user-permission.md)和 SQL Server 数据库用户登录名

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ RStudio 或包含 R 的内置 RGUI 工具等 IDE

若要本地和远程计算上下文之间来回切换，您需要两个系统。 本地通常是具有足够的电源可用于数据科学工作负荷的开发工作站。 远程在这种情况下是 SQL Server 2017 或 SQL Server 2016 与启用了 R 功能。 

切换计算上下文的前提是具有相同版本**RevoScaleR**本地和远程系统上。 在本地工作站上，可以获取**RevoScaleR**包和相关的提供程序，通过安装 Microsoft R 客户端。

如果你需要将客户端和服务器放在同一计算机上，请务必安装另一组用于从"远程"客户端发送 R 脚本的 Microsoft R 库。 不要使用 SQL Server 实例的程序文件中安装的 R 库。 具体而言，如果使用一台计算机，则需要**RevoScaleR**两个来支持客户端和服务器操作这些位置中的库。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

有关客户端配置的说明，请参阅[设置 R 开发数据科学客户端](../r/set-up-a-data-science-client.md)。


## <a name="r-development-tools"></a>R 开发工具

R 开发人员通常使用 Ide，用于编写和调试 R 代码。 一些建议如下：

- **针对 Visual Studio 的 R 工具**(RTVS) 是一种免费插件，提供 Intellisense、 调试、 和支持 Microsoft。您可以将其用于 R Server 和 SQL Server 机器学习服务。 若要下载，请参阅 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)。

- **RStudio** 是广受欢迎的 R 开发环境之一。 有关详细信息，请参阅[ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/)。

- 在 SQL Server 或 R 客户端安装 R 时，默认情况下也安装基本的 R 工具 (R.exe、 RTerm.exe、 RScripts.exe)。 如果不想安装 IDE，可以使用内置的 R 工具要在本教程中执行的代码。

请记住， **RevoScaleR**需在本地和远程计算机上。 无法完成本教程中使用的 RStudio 或其他环境，缺少 Microsoft R 库通用安装。 有关详细信息，请参阅 [设置数据科学客户端](../r/set-up-a-data-science-client.md)。

## <a name="summary-of-tasks"></a>任务的摘要

+ 数据最初是从 CSV 文件或 XDF 文件中获取的。 数据导入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用中的函数**RevoScaleR**包。
+ 使用执行模型定型和计分[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算上下文。 
+ 使用**RevoScaleR**函数来创建新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表以保存计分结果。
+ 在服务器上创建这两个绘图和本地计算上下文。
+ 中的数据对模型进行定型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中运行 R 的数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。
+ 提取数据的子集，并将其保存为 XDF 文件，以便在分析中重复使用在本地工作站上。
+ 获取新数据评分，通过打开 ODBC 连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 在本地工作站上进行评分。
+ 创建自定义 R 函数，然后运行该服务器中计算上下文执行模拟。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [第 1 课：创建数据库和权限](deepdive-work-with-sql-server-data-using-r.md)