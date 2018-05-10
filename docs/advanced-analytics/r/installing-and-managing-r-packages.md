---
title: 默认 SQL Server R 和 SQL Server 机器学习中的 R 和 Python 包库 |Microsoft 文档
description: 通过 SQL Server R Services，R Server 机学习服务 （数据库中） 和机器学习 Server （独立） 安装的 R 和 Python 包
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ee2c8124cf3487ca300c0b08ea113c8e66b114f4
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="default-r-and-python-packages-in-sql-server"></a>SQL Server 中的默认 R 和 Python 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何包库、 位置和与 SQL Server 安装的 R 和 Python 包的版本。 

## <a name="using-the-default-instance-library"></a>使用默认实例库

当你使用 SQL Server 安装机器学习时，请在你安装的每种语言的实例级别创建单个包库。 

所有的脚本或代码，运行中的 SQL Server 上数据库必须从实例库加载函数。 SQL Server 无法访问包安装到其他库。 这适用于以及远程客户端。 当从远程客户端连接到服务器，你想要在 server 计算上下文中运行任何 R 或 Python 代码只能使用包安装在实例库。

若要保护服务器资产，将默认实例库安装到受保护的文件夹注册到 SQL Server 并且可修改只能由计算机管理员。 如果你不是计算机的所有者，你可能需要获得管理员才能将包安装到此库的权限。 

即使你拥有计算机，将程序包添加到实例库之前应考虑在服务器环境中任何特定 R 或 Python 包的用途。 考虑因素，例如包文件和需求的多个版本的大小以及包需要网络或 internet 访问。

### <a name="in-database-engine-instance-file-paths"></a>数据库引擎实例的文件路径

下表显示 R 和 Python 的文件位置的版本和数据库引擎实例组合。 

|版本 | 实例名|默认路径|
|--------|--------------|------------|
| SQL Server 2016 |默认实例 (default instance)| C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library|
| SQL Server 2016 |命名实例 (named instance) | C:\Program Files\Microsoft SQL Server\MSSQL13。 < 实例名称 > \R_SERVICES\library|
| 使用 R 的 SQL Server 自 2017 年 1|默认实例 (default instance) | C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\library |
| 使用 R 的 SQL Server 自 2017 年 1|命名实例 (named instance)| C:\Program Files\Microsoft SQL Server\MSSQL14。MyNamedInstance\R_SERVICES\library |
| SQL Server 自 2017 年 Python |默认实例 (default instance) | C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\library |
| SQL Server 自 2017 年 Python|命名实例 (named instance)| C:\Program Files\Microsoft SQL Server\MSSQL14。 < 实例名称 > \PYTHON_SERVICES\library |

### <a name="standalone-server-file-paths"></a>独立服务器文件路径 

安装了 SQL Server 2016 R Server （独立） 或 SQL Server 自 2017 年 1 机器学习 Server （独立） 服务器时下, 表列出的二进制文件的默认路径。 

|版本| 安装|默认路径|
|------|------|------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|机器学习服务器，使用 R |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|机器学习 Python 具有服务器 |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> 如果您发现具有类似的子文件夹名称和文件的其他文件夹，你可能具有 Microsoft R Server 的独立安装或[机器学习服务器](https://docs.microsoft.com/machine-learning-server/)。 这些服务器产品具有不同的安装程序和路径 （即，C:\Program Files\Microsoft\R Server\R_SERVER 或 C:\Program Files\Microsoft\ML SERVER\R_SERVER）。 有关详细信息，请参阅[安装机器学习用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)或[适用于 Windows 中安装 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

## <a name="what-is-included-in-a-default-installation"></a>默认安装中包含的内容

本部分总结了 R 和 Python 默认安装中包括的功能。

### <a name="r-components"></a>R 组件

组件包括 Microsoft 的开放源代码 R 作为分布[Microsoft R Open](https://mran.microsoft.com/open)。 基本 R 包包括核心功能，如**统计信息**和**utils**。 你可以运行`installed.packages(priority = "base")`返回的包列表。 基础安装的 R 还包括大量样本数据集，以及标准的 R 工具，如 RGui （轻量交互式编辑器） 和 RTerm （R 命令提示符）。

Microsoft 包中包含[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)为远程计算上下文，流式处理，并行执行的数据导入和转换的 rx 函数，建模，可视化效果和分析。 [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)添加机器学习建模中。其他包包括[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)用于在 R 中，编写 MDX 语句和[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)用于在存储过程中包括 R 脚本。


|发行版本             | R 版本       | Microsoft 包    |
|--------------------|-----------------|-----------------------|
| SQL Server 2016 R Services | 3.2.2   | RevoScaleR sqlrutil  |
| SQL Server 2017 机器学习服务| 3.4.3 | RevoScaleR，MicrosoftML，olapR sqlrutil|

可以将包和预安装的模型添加到 SQL Server 2016 R Services 通过绑定到现代的生命周期支持策略。 绑定更改服务的模式。 默认情况下，初始安装后，R 包刷新一次通过 service pack 和累积更新。 其他包和核心 R 组件的完整版本升级才有可能通过产品升级 （从 SQL Server 2017 到 SQL Server 2016) 或通过将绑定 R 支持到 Microsoft 机器学习服务器。 有关详细信息，请参阅[中 SQL Server 的升级 R 和 Python 组件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="python-components"></a>Python 组件

SQL Server 2017 添加 Python 组件。 当选择 Python 语言选项时，则会安装 Anaconda 分发。 Python 代码库，除了标准安装包括示例数据、 单元测试和示例脚本。 

Microsoft 包中包含[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)为流式处理，Python 等效的 RevoScaleR，并行的数据导入和转换、 建模、 可视化和分析的 rx 函数的执行。 另一个 Python 包是[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)培训和转换、 评分、 文本和图像分析和提取特征用于从现有数据派生值。

SQL Server 自 2017 年 1 机器学习是具有 R 和 Python 支持的第一个版本。

|发行版本             | Anaconda 版本| Microsoft 包    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 机器学习服务  | 通过 Python 3.5 4.2 | revoscalepy microsoftml |

初始安装后 Python 包刷新通过 service pack 和累积更新，但完整的版本升级仅可以通过将 Python 支持绑定到 Microsoft 机器学习服务器。 有关详细信息，请参阅[中 SQL Server 的升级 R 和 Python 组件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="administrative-permissions-for-package-installation"></a>包安装的管理权限

包安装所需的权限更改 SQL Server 2016 和 SQL Server 自 2017 年之间。

+ SQL Server 2016 中管理访问权限是新的 R 包安装所必需的。
+ 在 SQL Server 自 2017 年，你可以继续以管理员身份安装包，R 和 Python，和这很可能是最简单的方法。 

    DDL 语句，创建外部库，允许数据库管理员，而无需使用 R 工具安装包。 

    如果对机器学习服务器使用程序包管理功能，你可以使用 RevoScaleR 安装在数据库级别的 R 包。 数据库管理员必须启用功能，然后向用户授予他们自己的软件包安装基于每个数据库的能力。 有关详细信息，请参阅[启用包管理使用 Ddl](r-package-how-to-enable-or-disable.md)。

### <a name="user-libraries-are-not-supported"></a>不支持用户库

用户不能将程序包安装到安全的位置，通常采用到用户库安装程序包。 但是，这是不可能在 SQL Server 环境中。 文件系统访问通常被限制在服务器上，且在 SQL Server 中执行外部脚本运行时即使到服务器上的用户文档文件夹具有管理员权限和访问权限，无法访问安装默认实例之外的任何包库。 但是，可能会解决方法。 有关如何解决与用户库相关的问题的提示，请参阅[解决方法的 R 用户库](packages-installed-in-user-libraries.md)。

## <a name="next-steps"></a>后续步骤

+ [获取包信息](determine-which-packages-are-installed-on-sql-server.md)
+ [安装新的 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新的 Python 软件包](../python/install-additional-python-packages-on-sql-server.md)
+ [启用远程 R 包管理](r-package-how-to-enable-or-disable.md)
+ [用于 R 程序包管理 RevoScaleR 函数](use-revoscaler-to-manage-r-packages.md)
+ [R 包同步](package-install-uninstall-and-sync.md)
+ [本地 R 程序包存储库的 miniCRAN](create-a-local-package-repository-using-minicran.md)
