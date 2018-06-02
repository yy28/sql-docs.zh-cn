---
title: 默认 SQL Server R 和 SQL Server 机器学习中的 R 和 Python 包库 |Microsoft 文档
description: 通过 SQL Server R Services，R Server 机学习服务 （数据库中） 和机器学习 Server （独立） 安装的 R 和 Python 包
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9362d6e9dc98f80beabc301f43e755b205b40a10
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707285"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>SQL Server 中的默认 R 和 Python 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文列出了与 SQL Server 以及在何处查找包库一起安装的 R 和 Python 包。  

## <a name="r-package-list-for-sql-server"></a>SQL Server 的 R 包列表

与安装 R 包[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)和[SQL Server 自 2017 年 1 机器学习 Services](../install/sql-machine-learning-services-windows-install.md)当 R 功能选择在安装过程。 

包         | 2016 | 2017 | Description |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | 用于远程计算上下文，流式处理的数据导入和转换、 建模、 可视化和分析的 rx 函数的并行执行。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |用于存储过程中包括 R 脚本。 |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.2 | 添加机器学习算法中。 | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a.  | 9.2 | 用于编写 MDX 语句中。 |

默认情况下，SQL Server 自 2017 年 1 机器学习 Services 中有 MicrosoftML 和 olapR。 在 SQL Server 2016 R Services 实例中，您可以添加通过这些包[组件升级](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。 组件升级也获取较新版本的包 （例如，较新版本的 RevoScaleR 包括用于 SQL Server 上的程序包管理的函数）。

## <a name="python-package-list-for-sql-server"></a>SQL Server 的 Python 包列表

在安装时，将仅在 SQL Server 2017 提供 Python 程序包[SQL Server 自 2017 年 1 机器学习 Services](../install/sql-machine-learning-services-windows-install.md) ，然后选择 Python 功能。

| 包         | 2017    |  Description |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 用于远程计算上下文，流式处理的数据导入和转换、 建模、 可视化和分析的 rx 函数的并行执行。 |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | 在 Python 中添加机器学习算法。 |

## <a name="open-source-r-in-your-installation"></a>在安装过程中的开放源代码 R

R 支持包括开放源代码，以便你可以调用基础 R 函数，并安装其他第三方和开放源代码包。 R 语言支持包括核心功能，如**基**，**统计信息**， **utils**，和其他人。 基础安装的 R 还包括大量示例数据集和标准 R 工具，例如**RGui** （轻量交互式编辑器） 和**RTerm** （R 命令提示符）。 

你安装中包括的开放源代码 R 分布是[Microsoft R 打开 (MRO)](https://mran.microsoft.com/open)。 MRO 通过其中包括其他开源包，例如将值添加到基 R [Intel 数学内核库](https://en.wikipedia.org/wiki/Math_Kernel_Library)。

下表总结了 R MRO 使用 SQL Server 安装程序提供的版本。

|发行版本             | R 版本       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 自 2017 年 1 机器学习服务](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

你应永远不会手动覆盖 R SQL Server 安装程序使用在 web 上找到的较新版本安装的版本。 基于 Microsoft R 包在特定版本的。 修改你的安装可能导致不稳定它。

## <a name="open-source-python-in-your-installation"></a>在安装过程中的开放源代码 Python

SQL Server 2017 添加 Python 组件。 当选择 Python 语言选项时，则会安装 Anaconda 4.2 分发。 Python 代码库，除了标准安装包括示例数据、 单元测试和示例脚本。 

SQL Server 自 2017 年 1 机器学习是具有 R 和 Python 支持的第一个版本。

|发行版本             | Anaconda 版本| Microsoft 包    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 机器学习服务  | 通过 Python 3.5 4.2 | revoscalepy microsoftml |

你应永远不会手动覆盖 SQL Server 安装程序安装在 web 上找到的较新版本的 Python 的版本。 Microsoft Python 包基于 Anaconda 的特定版本。 修改你的安装可能导致不它的稳定。

## <a name="component-upgrades"></a>组件升级

初始安装后，R 和 Python 包刷新通过 service pack 和累积更新，但仅可以通过完整版本升级*绑定*现代生命周期支持策略。 绑定更改服务的模式。 默认情况下，初始安装后，R 包刷新一次通过 service pack 和累积更新。 其他包和核心 R 组件的完整版本升级才有可能通过产品升级 （从 SQL Server 2017 到 SQL Server 2016) 或通过将绑定 R 支持到 Microsoft 机器学习服务器。 有关详细信息，请参阅[中 SQL Server 的升级 R 和 Python 组件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="package-library-location"></a>包库位置

当你使用 SQL Server 安装机器学习时，请在你安装的每种语言的实例级别创建单个包库。 在 Windows 上，实例库是受保护的文件夹注册到 SQL Server。

所有的脚本或代码，运行中的 SQL Server 上数据库必须从实例库加载函数。 SQL Server 无法访问包安装到其他库。 这适用于以及远程客户端。 当从远程客户端连接到服务器，你想要在 server 计算上下文中运行任何 R 或 Python 代码只能使用包安装在实例库。

若要保护服务器资产，可以仅由计算机管理员修改默认实例库。 如果你不是计算机的所有者，你可能需要获得管理员才能将包安装到此库的权限。 

#### <a name="file-path-for-in-database-engine-instances"></a>在数据库引擎实例的文件路径

下表显示 R 和 Python 的文件位置的版本和数据库引擎实例组合。 MSSQL13 表示 SQL Server 2016，它是仅 R。 SQL Server 2017 MSSQL14 并且 R 和 Python 的文件夹。 

文件路径还包括实例名称。 SQL Server 安装[数据库引擎实例的](../../database-engine/configure-windows/database-engine-instances-sql-server.md)作为默认实例 (MSSQLSERVER) 或用户定义的命名实例。 如果作为命名实例安装 SQL Server，你将看到该名称，如下所示追加： `MSSQL13.<instance_name>`。

|版本和语言  | 默认路径|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library|
| 使用 R 的 SQL Server 自 2017 年 1|C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\library |
| SQL Server 自 2017 年 Python |C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Lib\site 包 |


#### <a name="file-path-for-standalone-server-installations"></a>独立服务器安装的的文件路径

安装了 SQL Server 2016 R Server （独立） 或 SQL Server 自 2017 年 1 机器学习 Server （独立） 服务器时下, 表列出的二进制文件的默认路径。 

|版本| 安装|默认路径|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|机器学习服务器，使用 R |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|机器学习 Python 具有服务器 |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> 如果您发现具有类似的子文件夹名称和文件的其他文件夹，你可能具有 Microsoft R Server 的独立安装或[机器学习服务器](https://docs.microsoft.com/machine-learning-server/)。 这些服务器产品具有不同的安装程序和路径 （即，C:\Program Files\Microsoft\R Server\R_SERVER 或 C:\Program Files\Microsoft\ML SERVER\R_SERVER）。 有关详细信息，请参阅[安装机器学习用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)或[适用于 Windows 中安装 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

## <a name="next-steps"></a>后续步骤

+ [获取包信息](determine-which-packages-are-installed-on-sql-server.md)
+ [安装新 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [启用远程 R 包管理](r-package-how-to-enable-or-disable.md)
+ [用于 R 包管理的 RevoScaleR 函数](use-revoscaler-to-manage-r-packages.md)
+ [R 包同步](package-install-uninstall-and-sync.md)
+ [本地 R 包存储库的 miniCRAN](create-a-local-package-repository-using-minicran.md)
