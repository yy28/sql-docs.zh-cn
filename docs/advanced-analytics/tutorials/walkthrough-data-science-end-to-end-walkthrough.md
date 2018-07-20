---
title: 适用于 R 和 SQL Server 的端到端数据科学演练 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3d4f38fd424c881392d48b0a6a24feb7f7e27ee0
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086499"
---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>适用于 R 和 SQL Server 的端到端数据科学演练
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本演练中，您开发基于 SQL Server 2016 或 SQL Server 2017 中 R 功能支持的预测性建模的端到端解决方案。

此演练基于常用的公共数据集，即纽约市出租车数据集。 使用 R 代码的组合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据和自定义 SQL 函数，来生成分类模型，该值指示该驱动程序可能会在特定出租车行程小费的概率。 您还部署 R 模型到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并使用服务器数据来生成基于模型的分数。

此示例中可以扩展到所有类型的现实问题，例如预测客户对销售市场活动的响应或预测支出或在活动的出席情况。 因为可以从存储过程调用模型，可以轻松地将其嵌入应用程序中。

因为本演练旨在向 R 开发人员介绍[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，只要有可能使用 R。 但是，这并不意味着 R 一定是每个任务的最佳工具。 在许多情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会提供更好的性能，特别是对于诸如数据聚合和特征工程这类任务。  这类任务可以特别受益于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的新功能，如内存优化的列存储索引。 我们尝试指出的是在此过程可能的优化。

## <a name="target-audience"></a>目标受众

此演练面向 R 或 SQL 开发人员。 它提供了如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 将 R 集成到企业工作流的简介。  您应熟悉数据库操作，例如创建数据库和表、 导入数据，并运行查询。

+ 包含所有 SQL 和 R 脚本都。
+ 您可能需要修改脚本，在您的环境中运行中的字符串。 你可以使用任何代码编辑器，如[Visual Studio Code](https://code.visualstudio.com/Download)。

## <a name="prerequisites"></a>必要條件

我们建议本演练在便携式计算机或其他计算机上已安装的 Microsoft R 库。 您必须能够连接，在同一网络上为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 SQL Server 和 R 语言已启用的计算机。

您可以同时具有的计算机上运行演练[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 R 开发环境，但我们不建议此配置适用于生产环境。

如果你想要从远程计算机，如便携式计算机或其他联网的计算机运行 R 命令，则必须安装 Microsoft R Open 库。 可以安装 Microsoft R Client 或 Microsoft R Server。 在远程计算机必须能够连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。

如果你需要将客户端和服务器放在同一计算机上，请务必安装一组单独的用于使用 Microsoft R 库中从"远程"客户端发送 R 脚本。 请不要用于安装的 R 库使用由 SQL Server 实例实现此目的。

## <a name="add-r-to-sql-server"></a>将 R 添加到 SQL Server

您必须具有对安装 R 的支持的 SQL Server 实例访问。 本演练最初是针对 SQL erver 2016 开发和测试 2017 起，因此您应能够使用以下 SQL Server 版本之一。 （有 RevoScaleR 函数在各版本之间的一些小差异。）

+ [安装 SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)
+ [安装 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)。

## <a name="install-an-r-development-environment"></a>安装 R 开发环境

对于本演练中，我们建议你使用 R 开发环境。 以下是一些建议：

- **针对 Visual Studio 的 R 工具**(RTVS) 是一种免费插件，它提供 Intellisense、 调试、 并对 Microsoft。 您可以将其用于 R Server 和 SQL Server 机器学习服务的支持。 若要下载，请参阅 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)。

- **Microsoft R Client**是一个轻型开发工具，支持在 R 中使用 RevoScaleR 包开发。 若要了解此工具，请参阅 [Microsoft R 客户端入门](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)。

- **RStudio** 是广受欢迎的 R 开发环境之一。 有关详细信息，请参阅[ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/)。

    无法完成本教程中使用的通用安装 RStudio 或其他环境中;您还必须为 Microsoft R Open 安装 R 包和连接库。 有关详细信息，请参阅 [设置数据科学客户端](../r/set-up-a-data-science-client.md)。

- 在 SQL Server 或 R 客户端安装 R 时，默认情况下也安装基本的 R 工具 (R.exe、 RTerm.exe、 RScripts.exe)。 如果不想安装 IDE，可以使用这些工具。

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>获取对 SQL Server 实例和数据库的权限

若要连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]运行脚本和上传数据，必须具有有效登录名的数据库服务器上。  可以使用 SQL 登录凭据或集成 Windows 身份验证信息。 请求数据库管理员，使用： 在数据库中配置以下权限的帐户

- 创建数据库、表、函数和存储过程
- 将数据写入到表
- 运行 R 脚本的能力 (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

对于本演练，我们可以使用 SQL 登录名**RTestUser**。 我们通常建议使用 Windows 集成身份验证，但出于某些演示目的使用 SQL 登录名是更简单。

## <a name="next-steps"></a>后续步骤

[使用 PowerShell 对数据进行准备](walkthrough-prepare-the-data.md)
