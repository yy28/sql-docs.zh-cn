---
title: 让数据科学家使用 R 语言的 SQL Server 机器学习教程
description: 本教程演示如何创建数据库内分析的端到端 R 解决方案。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0b1820e15975ca027af7b51e809ba920af3ffc82
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511295"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>教程：适用于 R 数据科学家的 SQL 开发
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本教程中让数据科学家，了解如何生成基于 SQL Server 2016 或 SQL Server 2017 中 R 功能支持的预测性建模的端到端解决方案。 本教程使用[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)上 SQL Server 数据库。 

使用 R 代码的组合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据和自定义 SQL 函数，来生成分类模型，该值指示该驱动程序可能会在特定出租车行程小费的概率。 您还部署 R 模型到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并使用服务器数据来生成基于模型的分数。

此示例中可以扩展到所有类型的现实问题，例如预测客户对销售市场活动的响应或预测支出或在活动的出席情况。 因为可以从存储过程调用模型，可以轻松地将其嵌入应用程序中。

因为本演练旨在向 R 开发人员介绍[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，只要有可能使用 R。 但是，这并不意味着 R 一定是每个任务的最佳工具。 在许多情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会提供更好的性能，特别是对于诸如数据聚合和特征工程这类任务。  这类任务可以特别受益于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的新功能，如内存优化的列存储索引。 我们尝试指出的是在此过程可能的优化。

## <a name="prerequisites"></a>先决条件

+ [与 R 集成的 SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md#verify-installation)或[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

+ [数据库权限](../security/user-permission.md)和 SQL Server 数据库用户登录名

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [NYC 出租车演示数据库](demo-data-nyctaxi-in-sql.md)

+ R IDE，例如 RStudio 或包含 R 的内置 RGUI 工具

我们建议本演练中，客户端工作站上。 您必须能够连接，在同一网络上为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 SQL Server 和 R 语言已启用的计算机。 有关工作站配置的说明，请参阅[设置 R 开发数据科学客户端](../r/set-up-a-data-science-client.md)。

或者，可以同时具有的计算机上运行演练[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 R 开发环境，但我们不建议此配置适用于生产环境。 如果你需要将客户端和服务器放在同一计算机上，请务必安装另一组用于从"远程"客户端发送 R 脚本的 Microsoft R 库。 不要使用 SQL Server 实例的程序文件中安装的 R 库。 具体而言，如果使用一台计算机，则需要在这种以支持客户端和服务器操作这些位置的 RevoScaleR 库。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>其他 R 包

本演练需要未安装默认情况下作为的一部分的多个 R 库[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 您必须在客户端上安装这两个包，在开发解决方案，以及在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将解决方案部署的计算机。

### <a name="on-a-client-workstation"></a>客户端工作站上

在 R 环境中，将以下行复制并在控制台窗口 （Rgui 或 IDE） 中执行代码。 某些包还会安装所需的包。 在所有，安装大约 32 个包。 必须具有 internet 连接才能完成此步骤。
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>在服务器上

必须为 SQL Server 上安装包的多个选项。 例如，SQL Server 提供了[R 包管理](../r/install-additional-r-packages-on-sql-server.md)，数据库管理员可以创建包存储库以及分配权限以安装其自己的包的用户的功能。 但是，如果您是计算机上的管理员，你可以安装使用 R，新的包，只要您将安装到正确的库。

> [!NOTE]
> 在服务器上**不这样做**即使系统提示您安装到用户库。 如果在安装到用户库，SQL Server 实例无法找到或运行包。 有关详细信息，请参阅[SQL Server 上安装新的 R 包](../r/install-additional-r-packages-on-sql-server.md)。

1. 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上，**以管理员身份**打开 RGui.exe。  如果已安装 SQL Server R Services 使用的默认设置，可以在 C:\Program Files\Microsoft SQL Server\MSSQL13 中找到 Rgui.exe。MSSQLSERVER\R_SERVICES\bin\x64)。

2. 在 R 提示符处，运行下面的 R 命令：
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  此示例使用 R grep 函数搜索可用路径的向量，并查找包括"Program Files"的路径。 有关详细信息，请参阅[ https://www.rdocumentation.org/packages/base/functions/grep ](https://www.rdocumentation.org/packages/base/functions/grep)。

  如果您认为已安装的软件包，通过运行检查已安装的包列表`installed.packages()`。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [浏览和汇总数据](walkthrough-view-and-summarize-data-using-r.md)