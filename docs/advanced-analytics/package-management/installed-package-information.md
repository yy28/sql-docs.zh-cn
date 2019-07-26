---
title: 默认 R 和 Python 包库
description: R 和 Python 包安装 SQL Server 适用于 R Services、R Server、机器学习服务 (数据库内) 和 Machine Learning Server (独立)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2a149b4a98ec6c3a1d35cb499dcd391d87216752
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470263"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>SQL Server 中的默认 R 和 Python 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文列出了随 SQL Server 安装的 R 和 Python 包, 以及在何处可以找到包库。  

## <a name="r-package-list-for-sql-server"></a>SQL Server 的 R 包列表

如果在安装过程中选择 R 功能, 则 r 包与[SQL Server 2016 r 服务](../install/sql-r-services-windows-install.md)和[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)一起安装。 

|包         | 2016 | 2017 | 描述 |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | 用于远程计算上下文、流式处理、用于数据导入和转换、建模、可视化和分析的 rx 函数的并行执行。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |用于在存储过程中包含 R 脚本。 |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.2 | 在 R 中添加机器学习算法。 | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a.  | 9.2 | 用于在 R 中编写 MDX 语句。 |

默认情况下, MicrosoftML 和 olapR 在 SQL Server 2017 机器学习服务中可用。 在 SQL Server 2016 R Services 实例上, 可以通过[组件升级](../install/upgrade-r-and-python.md)添加这些包。 组件升级还会获取较新版本的包 (例如, 较新版本的 RevoScaleR 包含 SQL Server 上的包管理功能)。

## <a name="python-package-list-for-sql-server"></a>SQL Server 的 Python 包列表

当你安装[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)并选择 python 功能时, python 包仅在 SQL Server 2017 中提供。

| 包         | 2017    |  描述 |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 用于远程计算上下文、流式处理、用于数据导入和转换、建模、可视化和分析的 rx 函数的并行执行。 |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | 在 Python 中添加机器学习算法。 |

## <a name="open-source-r-in-your-installation"></a>安装中的开源 R

R 支持包括开源, 因此你可以调用基本 R 函数并安装其他开源和第三方包。 R 语言支持包括**基本**、**统计**、 **utils**等核心功能。 R 的基本安装还包括多个示例数据集和标准的 R 工具, 例如**rgui.exe** (一种轻型交互式编辑器) 和**rterm.exe** (R 命令提示符)。 

安装中包含的开源 R 的分发是[Microsoft R open (MRO)](https://mran.microsoft.com/open)。 MRO 通过包含附加开源包 (如[Intel 数学内核库](https://en.wikipedia.org/wiki/Math_Kernel_Library)), 将值添加到基本 R。

下表总结了 MRO 使用 SQL Server 安装程序提供的 R 版本。

|发行版本             | R 版本       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

切勿手动覆盖通过 web 上的更新版本 SQL Server 安装程序安装的 R 版本。 Microsoft R 包基于特定版本的 R。修改安装可能会使其不稳定。

## <a name="open-source-python-in-your-installation"></a>安装中的开放源代码 Python

SQL Server 2017 添加 Python 组件。 选择 Python 语言选项时, 会安装 Anaconda 4.2 分发版。 除了 Python 代码库以外, 标准安装还包括示例数据、单元测试和示例脚本。 

SQL Server 2017 机器学习是支持 R 和 Python 的第一版。

|发行版本             | Anaconda 版本| Microsoft 包    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 机器学习服务  | 4.2 over Python 3。5 | revoscalepy、microsoftml |

切勿手动覆盖 SQL Server 安装程序安装了 web 上的更新版本。 Microsoft Python 包基于 Anaconda 的特定版本。 修改安装会使其不稳定。

## <a name="component-upgrades"></a>组件升级

初始安装后, 通过 service pack 和累积更新刷新 R 和 Python 包, 但仅可以通过*绑定*到新式生命周期支持策略来进行完整版本升级。 绑定将更改服务模型。 默认情况下, 在初始安装后, R 包通过 service pack 和累积更新进行刷新。 仅可通过产品升级 (从 SQL Server 2016 到 SQL Server 2017) 或将 R 支持绑定到 Microsoft Machine Learning Server, 来实现核心 R 组件的其他包和完整版本升级。 有关详细信息, 请参阅[SQL Server 中的升级 R 和 Python 组件](../install/upgrade-r-and-python.md)。

## <a name="package-library-location"></a>包库位置

如果使用 SQL Server 安装机器学习, 则会在实例级别为你安装的每种语言创建一个包库。 在 Windows 上, 实例库是 SQL Server 注册的安全文件夹。

在 SQL Server 上运行的所有脚本或代码都必须从实例库中加载函数。 SQL Server 无法访问安装到其他库的包。 这也适用于远程客户端。 从远程客户端连接到服务器时, 要在服务器计算上下文中运行的任何 R 或 Python 代码只能使用在实例库中安装的包。

若要保护服务器资产, 只能由计算机管理员修改默认实例库。 如果您不是计算机的所有者, 则您可能需要获得管理员权限才能将包安装到此库中。 

#### <a name="file-path-for-in-database-engine-instances"></a>数据库内引擎实例的文件路径

下表显示了 R 和 Python 的文件位置, 用于版本和数据库引擎实例组合。 MSSQL13.MSSQLSERVER 指示 SQL Server 2016, 并且为仅 R。 MSSQL14. 指示 SQL Server 2017, 并且具有 R 和 Python 文件夹。 

文件路径还包括实例名称。 SQL Server 将[数据库引擎实例](../../database-engine/configure-windows/database-engine-instances-sql-server.md)作为默认实例 (MSSQLSERVER) 或用户定义的命名实例安装。 如果 SQL Server 作为命名实例安装, 你将看到该名称追加如下: `MSSQL13.<instance_name>`。

|版本和语言  | 默认路径|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library|
| SQL Server 2017 与 R|C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 与 Python |C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages |


#### <a name="file-path-for-standalone-server-installations"></a>独立服务器安装的文件路径

下表列出了安装 SQL Server 2016 R Server (独立版) 或 SQL Server 2017 Machine Learning Server (独立) 服务器时, 二进制文件的默认路径。 

|Version| 安装|默认路径|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Machine Learning Server, with R |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Machine Learning Server, 具有 Python |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> 如果找到具有相似子文件夹名称和文件的其他文件夹, 则可能会独立安装 Microsoft R Server 或[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/)。 这些服务器产品具有不同的安装程序和路径 (即 C:\Program Files\Microsoft\R Server\R_SERVER 或 C:\Program Files\Microsoft\ML SERVER\R_SERVER)。 有关详细信息, 请参阅[安装 windows Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)或[安装适用于 Windows 的 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

## <a name="next-steps"></a>后续步骤

+ [获取包信息](installed-package-information.md)
+ [安装新 R 包](../r/install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [启用远程 R 包管理](../r/r-package-how-to-enable-or-disable.md)
+ [用于 R 包管理的 RevoScaleR 函数](../r/use-revoscaler-to-manage-r-packages.md)
+ [R 包同步](../r/package-install-uninstall-and-sync.md)
+ [本地 R 包存储库的 miniCRAN](../r/create-a-local-package-repository-using-minicran.md)
