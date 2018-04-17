---
title: 默认 SQL Server 上的机器学习的包库 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 64b085c2314e4c97694e91924cb15d43315143e0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="default-package-libraries-for-machine-learning-on-sql-server"></a>默认 SQL Server 上的机器学习的包库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍适用于 R 和与 SQL Server 安装的 Python 的默认库。 本文提供这些库的默认位置，并说明如何确定哪些包和 R 哪些版本或 Python 安装在每个实例库。

## <a name="using-the-default-instance-library"></a>使用默认实例库

当你使用 SQL Server 安装机器学习时，请在你安装的每种语言的实例级别创建单个包库。 SQL Server 无法访问包安装到其他库。

如果你从远程客户端连接到服务器，你想要在 server 计算上下文中运行任何 R 或 Python 代码可以使用仅安装在实例库中的包。

若要保护服务器资产，将默认实例库安装到受保护的文件夹注册到 SQL Server 并且可修改只能由计算机管理员。 如果你不是计算机的所有者，你可能需要获得管理员才能将包安装到此库的权限。 

即使你拥有计算机，将程序包添加到实例库之前应考虑在服务器环境中任何特定 R 或 Python 包的用途。 考虑因素，例如包文件和需求的多个版本的大小以及包需要网络或 internet 访问。

### <a name="sql-server"></a>SQL Server

|版本 | 实例名|默认路径|
|------|------|------|
| SQL Server 2016 |默认实例 (default instance)|`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`|
| SQL Server 2016 |命名实例 (named instance) |`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES\library`|
| 使用 R 的 SQL Server 自 2017 年 1|默认实例 (default instance) |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` |
| 使用 R 的 SQL Server 自 2017 年 1|命名实例 (named instance)|`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` |
| SQL Server 自 2017 年 Python |默认实例 (default instance) |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library` |
| SQL Server 自 2017 年 Python|命名实例 (named instance)|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES\library` |

### <a name="r-server-standalone-or-machine-learning-server-standalone"></a>R Server （独立） 或机器学习 Server （独立）

独立服务器安装使用 SQL Server 安装程序时，此表列出的二进制文件的默认路径。 

|版本| 安装|默认路径|
|------|------|------|
| SQL Server 2016|R Server (Standalone)| |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|机器学习服务器，使用 R |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|机器学习 Python 具有服务器 |`C:\Program Files\Microsoft SQL Server\130\PYTHON_SERVER`|

如果你安装 Microsoft R Server 或使用单独的 Windows installer 的机器学习服务器，默认路径是不同： 通常，其格式大致喜欢`C:\Program Files\Microsoft\R Server\R_SERVER`。 有关详细信息，请参阅：
 
+ [安装机器学习适用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [适用于 Windows 安装 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="what-is-included-in-a-default-installation"></a>默认安装中包含的内容

本部分提供默认安装的 R 或 Python 功能的摘要。

### <a name="default-r-installation-for-sql-server"></a>SQL Server 的默认 R 安装

默认情况下，R**基**安装包。 基本包包含核心功能提供通过包如`stats`和`utils`。

基础安装的 R 还包括大量样本数据集，以及标准的 R 工具，如 RGui （轻量交互式编辑器） 和 RTerm （R 命令提示符）。

安装 SQL Server 2016 或 SQL Server 自 2017 年中的 R 还包括**RevoScaleR**包和相关增强的包和提供程序，它支持远程计算上下文，流式处理，并行执行 rx 函数和许多其他功能。

若要升级 RevoScaleR 包，可以使用绑定来升级学习组件，计算机或修补程序或将您实例升级到较新版本的 SQL Server。

+ 增强的 R 功能的概述，请参阅[有关机器学习服务器](https://docs.microsoft.com/machine-learning-server/what-is-microsoft-r-server)

+ 若要下载到客户端计算机上的 RevoScaleR 库，安装[Microsoft R 客户端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

### <a name="default-python-installation-for-sql-server"></a>默认的 SQL Server 的 Python 安装

如果你选择机器学习功能和 Python 语言选项，已安装的 Anaconda 分布。 确切版本取决于已安装的 SQL Server 的版本和无论你是升级使用机器学习服务器安装程序的实例。

|发行版本| Anaconda 版本| 其他更改|
|------|------|------|
| SQL Server 2017 RTM| 3.5.2| 新： revoscalepy|
| 通过机器学习服务器 9.2.1 自 2017 年 9 月更新| Anaconda 4.2| 对 revoscalepy 更新 |
| SQL Server 2017 CU3| Anaconda 4.2| 对 revoscalepy 更新 |

Python 代码库，除了标准安装包括示例数据、 单元测试和示例脚本。

## <a name="restrictions-and-known-issues"></a>限制和已知的问题

可以使用在 SQL Server 中运行的任何解决方案**仅**安装在与实例关联的默认库中的包。

如果你使用绑定来升级实例中的 R 组件，可以更改实例库的路径。 请务必验证 SQL Server 当前使用的库路径。

## <a name="administrative-permissions-required-for-package-installation"></a>包安装所需的管理权限

包安装所需的权限更改 SQL Server 2016 和 SQL Server 自 2017 年之间。

+ SQL Server 2016 中管理访问权限是新的 R 包安装所必需的。

+ 在 SQL Server 自 2017 年，你可以继续以管理员身份安装包，R 和 Python，和这很可能是最简单的方法。

    DDL 语句，创建外部库，允许数据库管理员，而无需使用 R 工具安装包。 

    如果对机器学习服务器使用程序包管理功能，你可以使用 RevoScaleR 安装在数据库级别的 R 包。 数据库管理员必须启用功能，然后向用户授予他们自己的软件包安装基于每个数据库的能力。 有关详细信息，请参阅[启用包管理使用 Ddl](r-package-how-to-enable-or-disable.md)。

### <a name="user-libraries-are-not-supported"></a>不支持用户库

用户不能将程序包安装到安全的位置，通常采用到用户库安装程序包。 但是，这是不可能在 SQL Server 环境中。通常在服务器上限制甚至文件系统访问权限。

即使到服务器上的用户文档文件夹具有管理员权限和访问，在 SQL Server 中执行外部脚本运行时无法访问安装默认实例库之外的任何包。

有关如何解决与用户库相关的问题的提示，请参阅[包安装在用户库](packages-installed-in-user-libraries.md)。