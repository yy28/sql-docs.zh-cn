---
title: 本教程有关 RevoScaleR 函数与 SQL Server 机器学习 |Microsoft Docs
description: 在本教程中，了解如何调用 RevoScaleR 函数在使用支持 R 的 SQL Server 机器学习中启用。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4aa45d7ee690d55672c86be256e66d454860c2b6
ms.sourcegitcommit: b8e2e3e6e04368aac54100c403cc15fd4e4ec13a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2018
ms.locfileid: "45563869"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>教程： 使用 RevoScaleR R 函数与 SQL Server 数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 是用于数据科学和机器学习工作负荷提供分布式和并行处理的 Microsoft R 包。 SQL Server 中的 R 开发，RevoScaleR 是一个用于设置计算上下文，函数具有的核心内置包的管理包，最重要的是： 使用数据端到端，从导入到可视化和分析。 SQL Server 中的机器学习算法对 RevoScaleR 数据源的依赖项。 考虑到 RevoScaleR 的重要性，了解何时以及如何调用其函数是一项基本技能。 

在本教程中，将了解如何创建远程计算上下文，本地和远程计算上下文之间移动数据，并在远程 SQL 服务器上执行 R 代码。 你还了解如何分析和本地和远程服务器上绘制数据以及如何创建和部署模型。

+ 数据最初是从 CSV 文件或 XDF 文件中获取的。 导入数据到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]RevoScaleR 包中使用的函数。
+ 使用执行模型定型和计分[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算上下文。 
+ 使用 RevoScaleR 函数来创建新的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表以保存计分结果。
+ 在服务器上创建这两个绘图和本地计算上下文。
+ 中的数据对模型进行定型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中运行 R 的数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。
+ 提取数据的子集，并将其保存为 XDF 文件，以便在分析中重复使用在本地工作站上。
+ 获取新数据评分，通过打开 ODBC 连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 在本地工作站上进行评分。
+ 创建自定义 R 函数，然后运行该服务器中计算上下文执行模拟。

## <a name="target-audience"></a>目标受众

本教程旨在让数据科学家或于那些已有某种程度上熟悉 R 和数据科学任务，例如摘要和创建模型。 但是，所有代码已都提供，因此即使您不熟悉 R，可以运行该代码并按说明操作，假定您具有所需的服务器和客户端环境。

您还应熟悉[!INCLUDE[tsql](../../includes/tsql-md.md)]语法并知道如何访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库使用这些工具：

+ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 
+ Visual Studio 中的数据库工具 
+ 免费[适用于 Visual Studio Code 的 mssql 扩展](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)。
  
> [!TIP]
> 在各个课程之间保存 R 工作区，便可轻松地从中断的位置继续。

## <a name="prerequisites"></a>必要條件

- **支持 R 的 SQL Server**
  
    安装[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)使用 R 功能或安装[SQL Server 2016 R Services （数据库内）](../install/sql-r-services-windows-install.md)。

    请确保启用外部脚本、 快速启动板服务正在运行，并且你有权访问该服务。
  
-  **数据库权限**
  
    若要运行用于定型模型的查询，必须在存储数据的数据库上具有 **db_datareader** 权限。 若要运行 R，用户必须具有的权限 EXECUTE ANY EXTERNAL SCRIPT。

-   **数据科学开发计算机**
  
    若要本地和远程计算上下文之间来回切换，您需要两个系统。 本地通常是具有足够的电源可用于数据科学工作负荷的开发工作站。 远程在这种情况下是 SQL Server 2017 或 SQL Server 2016 与启用了 R 功能。 
    
    切换计算上下文的前提是在本地和远程系统上具有相同版本 RevoScaleR。 在本地工作站上，你可以获取的 RevoScaleR 包和相关的提供程序安装或使用以下任何一个：[在 Azure 上的数据科学 VM](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)， [（免费） 的 Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)，或[Microsoft Machine Learning Server （独立版）](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-install)。 对于独立服务器选项，请安装免费的开发人员版本，使用 Linux 或 Windows 安装程序。 此外可以使用 SQL Server 安装程序安装在独立服务器。
      
-   **其他 R 包**
  
    在本教程中，您将安装以下包： **dplyr**， **ggplot2**， **ggthemes**， **reshape2**，和**e1071**. 本教程提供说明。
  
    必须在两个位置安装所有包： 在用于 R 解决方案开发工作站上和执行 R 脚本所在的 SQL Server 计算机上。 如果没有在服务器计算机上安装包的权限，请让管理员。 
    
    **请勿将包安装到用户库。** 必须在 SQL Server 实例使用的 R 包库中安装包。

## <a name="r-development-tools"></a>R 开发工具

R 开发人员通常使用 Ide，用于编写和调试 R 代码。 一些建议如下：

- **针对 Visual Studio 的 R 工具**(RTVS) 是一种免费插件，提供 Intellisense、 调试、 和支持 Microsoft。您可以将其用于 R Server 和 SQL Server 机器学习服务。 若要下载，请参阅 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)。

- **RStudio** 是广受欢迎的 R 开发环境之一。 有关详细信息，请参阅[ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/)。

- 在 SQL Server 或 R 客户端安装 R 时，默认情况下也安装基本的 R 工具 (R.exe、 RTerm.exe、 RScripts.exe)。 如果不想安装 IDE，可以使用内置的 R 工具要在本教程中执行的代码。

前面曾提到，RevoScaleR 需要本地和远程计算机上。 无法完成本教程中使用的 RStudio 或其他环境，缺少 Microsoft R 库通用安装。 有关详细信息，请参阅 [设置数据科学客户端](../r/set-up-a-data-science-client.md)。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [第 1 课： 创建数据库和权限](deepdive-work-with-sql-server-data-using-r.md)

