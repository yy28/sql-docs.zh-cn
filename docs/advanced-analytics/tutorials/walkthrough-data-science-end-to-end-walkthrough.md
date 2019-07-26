---
title: 使用 R 语言的数据科学家教程
description: 介绍如何为数据库内分析创建端到端 R 解决方案的教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 072d2c2e8843b17b3a4ccfeed16bd0916ce501e7
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468637"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>教程：适用于 R 数据科学家的 SQL 开发
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本教程中, 对于数据科学家, 请了解如何基于 SQL Server 2016 或 SQL Server 2017 中的 R 功能支持生成用于预测建模的端到端解决方案。 本教程使用 SQL Server 上的[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)数据库。 

使用 R 代码、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据和自定义 SQL 函数的组合来构建一个分类模型, 该模型指示驱动程序可能在特定出租车行程上出现提示的概率。 你还可以将 R 模型部署[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到, 并使用服务器数据基于该模型生成分数。

可以将此示例扩展到各种真实的问题, 例如预测客户对销售活动的响应, 或预测发生事件的支出或出席情况。 由于可以从存储过程调用模型, 因此可以轻松地将其嵌入到应用程序中。

由于本演练旨在向 r 开发人员[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]介绍, 因此尽可能使用 r。 但是, 这并不意味着 R 一定是每个任务的最佳工具。 在许多情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会提供更好的性能，特别是对于诸如数据聚合和特征工程这类任务。  这类任务可以特别受益于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的新功能，如内存优化的列存储索引。 我们尝试在此过程中指出可能的优化。

## <a name="prerequisites"></a>先决条件

+ [SQL Server 2017 机器学习服务与 R 集成](../install/sql-machine-learning-services-windows-install.md#verify-installation)或[SQL Server 2016 r 服务](../install/sql-r-services-windows-install.md)

+ [数据库权限](../security/user-permission.md)和 SQL Server 数据库用户登录

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [NYC 出租车演示数据库](demo-data-nyctaxi-in-sql.md)

+ R IDE (如 RStudio) 或 R 附带的内置 RGUI.EXE 工具

建议你在客户端工作站上执行此操作。 您必须能够在同一网络上连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Server 且启用了 R 语言的计算机。 有关工作站配置的说明, 请参阅[设置用于 R 开发的数据科学客户端](../r/set-up-a-data-science-client.md)。

或者, 您可以在同时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有 R 开发环境的计算机上运行该演练, 但对于生产环境不建议使用此配置。 如果需要将客户端和服务器放在同一台计算机上, 请确保安装另一组 Microsoft R 库, 以便从 "远程" 客户端发送 R 脚本。 不要使用在 SQL Server 实例的 program 文件中安装的 R 库。 具体而言, 如果你使用一台计算机, 则需要在这两个位置都使用 RevoScaleR 库来支持客户端和服务器操作。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>其他 R 包

本演练需要多个默认情况下不作为的[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]一部分安装的 R 库。 你必须在开发解决方案的客户端和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]部署解决方案的计算机上安装这些包。

### <a name="on-a-client-workstation"></a>在客户端工作站上

在 R 环境中, 复制以下行, 并在控制台窗口中执行代码 (Rgui.exe 或 IDE)。 某些包还会安装所需的包。 毕竟, 安装了大约32个包。 你必须具有 internet 连接才能完成此步骤。
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>在服务器上

在 SQL Server 上安装包有多个选项。 例如, SQL Server 提供[R 包管理](../r/install-additional-r-packages-on-sql-server.md)功能, 使数据库管理员可以创建包存储库, 并为用户分配安装其自己的包的权限。 但是, 如果您是计算机上的管理员, 则只要您将安装到正确的库中, 就可以使用 R 安装新的包。

> [!NOTE]
> 在服务器**上, 即使**出现提示, 也不要安装到用户库。 如果安装到用户库, SQL Server 实例无法找到或运行包。 有关详细信息, 请参阅[SQL Server 上的 "安装新的 R 包"](../r/install-additional-r-packages-on-sql-server.md)。

1. 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上，**以管理员身份**打开 RGui.exe。  如果已使用默认值安装 SQL Server R Services, 则可在 C:\Program Files\Microsoft SQL Server\MSSQL13. 中找到 Rgui.exe。MSSQLSERVER\R_SERVICES\bin\x64).

2. 在 R 提示符处，运行下面的 R 命令：
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  此示例使用 R grep 函数搜索可用路径的向量, 并查找包含 "Program Files" 的路径。 有关详细信息, 请[https://www.rdocumentation.org/packages/base/functions/grep](https://www.rdocumentation.org/packages/base/functions/grep)参阅。

  如果你认为包已安装, 请通过运行`installed.packages()`来检查已安装包的列表。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [浏览并汇总数据](walkthrough-view-and-summarize-data-using-r.md)