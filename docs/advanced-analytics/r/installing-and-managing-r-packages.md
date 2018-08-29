---
title: 默认 SQL Server R 和 SQL Server 机器学习中的 R 和 Python 包库 |Microsoft Docs
description: 通过 SQL Server R Services，R Server 机器学习服务 （数据库内） 和机器学习服务器 （独立版） 安装的 R 和 Python 包
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7f5c51e9b93aca5d52858417667865633a0c4151
ms.sourcegitcommit: e4e9f02b5c14f3bb66e19dec98f38c012275b92c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2018
ms.locfileid: "43118305"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>SQL Server 中的默认 R 和 Python 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文列出了使用 SQL Server 和在哪里可以找到的包库安装的 R 和 Python 包。  

## <a name="r-package-list-for-sql-server"></a>适用于 SQL Server 的 R 包列表

使用安装 R 包[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)并[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)在安装期间选择 R 功能时。 

包         | 2016 | 2017 | Description |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | 用于远程计算上下文，流式处理的数据导入和转换、 建模、 可视化和分析的 rx 函数的并行执行。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |用于存储过程中包括 R 脚本。 |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.2 | 在 R 中添加机器学习算法 | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a.  | 9.2 | 用于在 R 中编写 MDX 语句 |

MicrosoftML 和 olapR 是默认情况下，SQL Server 2017 机器学习服务中可用。 上的 SQL Server 2016 R Services 实例，你可以添加这些包通过[组件升级](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。 组件升级也获取较新版本的包 （例如，较新版本的 RevoScaleR 包含用于 SQL Server 上的程序包管理的函数）。

## <a name="python-package-list-for-sql-server"></a>适用于 SQL Server 的 Python 包列表

在安装时，Python 包是仅在 SQL Server 2017 中提供[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)，然后选择 Python 功能。

| 包         | 2017    |  Description |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 用于远程计算上下文，流式处理的数据导入和转换、 建模、 可视化和分析的 rx 函数的并行执行。 |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | 在 Python 中添加机器学习算法。 |

## <a name="open-source-r-in-your-installation"></a>在安装中的开放源代码 R

R 支持包括开放源代码，以便可以调用基础 R 函数并安装其他的开源和第三方包。 R 语言支持包括核心功能，如**基**， **stats**， **utils**，等等。 R 的基本安装还包括许多示例数据集和标准 R 工具，例如**RGui** （轻量交互式编辑器） 和**RTerm** （R 命令提示符）。 

开放源代码 R 安装中包括的分布[Microsoft R 打开 (MRO)](https://mran.microsoft.com/open)。 MRO 由其中包括其他开放源代码包，例如将值添加到基本 R [Intel 数学内核库](https://en.wikipedia.org/wiki/Math_Kernel_Library)。

下表总结了由 MRO 使用 SQL Server 安装程序提供的 R 版本。

|发行版本             | R 版本       |
|--------------------|-----------------|
| [SQL Server 2016 R 服务](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

你应永远不会手动覆盖 SQL Server 安装程序安装在 web 上找到的较新版本的 R 的版本。 Microsoft R 包以在特定版本的。 修改您的安装可能会破坏稳定性它。

## <a name="open-source-python-in-your-installation"></a>在安装中的开源 Python

SQL Server 2017 添加 Python 组件。 当选择 Python 语言选项时，会安装 Anaconda 4.2 分发。 Python 代码库，除了标准安装包括示例数据、 单元测试和示例脚本。 

SQL Server 2017 机器学习是具有 R 和 Python 支持的第一个版本。

|发行版本             | Anaconda 版本| Microsoft 包    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 机器学习服务  | 通过 Python 3.5 4.2 | revoscalepy microsoftml |

你应永远不会手动覆盖由 SQL Server 安装程序安装在 web 上找到的较新版本的 Python 版本。 Microsoft Python 包基于特定版本的 Anaconda。 修改您的安装可能会破坏它的稳定性。

## <a name="component-upgrades"></a>组件升级

初始安装后，R 和 Python 包刷新通过 service pack 和累积更新，但完整的版本升级，才可以通过*绑定*到新式生命周期支持策略。 绑定更改服务模型。 默认情况下，初始安装后的 R 包刷新一次通过 service pack 和累积更新。 其他包和完整版本升级的核心 R 组件只能通过产品升级 （从 SQL Server 2016 到 SQL Server 2017) 或通过绑定 R 支持到 Microsoft Machine Learning Server。 有关详细信息，请参阅[SQL Server 中的升级 R 和 Python 组件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="package-library-location"></a>包库位置

当使用 SQL Server 安装机器学习时，请在实例级别为你安装每种语言创建单个包库。 在 Windows，实例库是注册到 SQL Server 受保护的文件夹。

所有脚本或代码的运行中的 SQL Server 上数据库必须从实例库都加载函数。 SQL Server 无法访问包安装到其他库。 这适用于以及远程客户端。 当从远程客户端连接到服务器，你想要在 server 计算上下文中运行任何 R 或 Python 代码只能使用实例库中安装的包。

若要保护服务器资产，默认实例库可以修改只能由计算机管理员。 如果您不是计算机的所有者，你可能需要从包安装到此库管理员获取权限。 

#### <a name="file-path-for-in-database-engine-instances"></a>在数据库引擎实例的文件路径

下表显示 R 和 Python 的文件位置的版本和数据库引擎实例组合。 MSSQL13 表示 SQL Server 2016，它是仅限 R 的。 SQL Server 2017 MSSQL14 并且 R 和 Python 文件夹。 

文件路径还包括实例名称。 SQL Server 安装[数据库引擎实例](../../database-engine/configure-windows/database-engine-instances-sql-server.md)作为默认实例 (MSSQLSERVER) 或用户定义的命名实例。 如果 SQL Server 作为命名实例安装，您将看到该名称后追加，如下所示： `MSSQL13.<instance_name>`。

|版本和语言  | 默认路径|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library|
| 使用 R 的 SQL Server 2017|C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\library |
| 与 Python 配合使用的 SQL Server 2017 |C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Lib\site 包 |


#### <a name="file-path-for-standalone-server-installations"></a>独立服务器安装的的文件路径

安装 SQL Server 2016 R Server （独立版） 或 SQL Server 2017 机器学习服务器 （独立版） 服务器时下, 表列出了二进制文件的默认路径。 

|版本| 安装|默认路径|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL server\130\r_server 位置|
|SQL Server 2017|机器学习服务器，使用 R |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|机器学习服务器，与 Python 配合使用 |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> 如果您发现其他具有类似的子文件夹名称和文件的文件夹，则可能出现的 Microsoft R Server 独立安装或[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/)。 这些服务器产品具有不同的安装程序和路径 （即 C:\Program Files\Microsoft\R Server\R_SERVER 或 C:\Program Files\Microsoft\ML SERVER\R_SERVER）。 有关详细信息，请参阅[的 Windows 安装机器学习服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)或[对于 Windows 中安装 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

## <a name="next-steps"></a>后续步骤

+ [获取包信息](determine-which-packages-are-installed-on-sql-server.md)
+ [安装新 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [启用远程 R 包管理](r-package-how-to-enable-or-disable.md)
+ [用于 R 包管理的 RevoScaleR 函数](use-revoscaler-to-manage-r-packages.md)
+ [R 包同步](package-install-uninstall-and-sync.md)
+ [本地 R 包存储库的 miniCRAN](create-a-local-package-repository-using-minicran.md)
