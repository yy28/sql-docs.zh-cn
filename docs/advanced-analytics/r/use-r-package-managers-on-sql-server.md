---
title: 使用 R 包管理器-SQL Server 机器学习服务
description: 使用标准 R 命令，如 install.packages 将新的 R 包添加到 SQL Server 2016 R Services 或 SQL Server 2017 机器学习服务 （数据库内）。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: d53725e708a5aaf6fb8476ce2d7408ffcfa7f102
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962404"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>使用 R 包管理器在 SQL Server 上安装 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

可以使用标准的 R 工具的 SQL Server 2016 实例上安装新包或 SQL Server 2017 中，提供在计算机已打开端口 80 并且具有管理员权限。

> [!IMPORTANT] 
> 请确保包安装到与当前实例关联的默认库。 永远不会将包安装到用户目录。

此过程使用 RGui，但可以使用 RTerm 或任何其他 R 命令行工具，它支持提升的访问权限。

## <a name="install-a-package-using-rgui"></a>使用 RGui 安装包

1. [确定实例库的位置](../package-management/default-packages.md)。 导航到安装的 R 工具的文件夹。 例如，SQL Server 2017 默认实例的默认路径如下所示： `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. 右键单击 RGui.exe，然后选择**以管理员身份运行**。 如果您没有所需的权限，请与数据库管理员联系并提供所需的包的列表。

1. 从命令行中，如果您知道包名称，则可以键入：`install.packages("the_package-name")` 两个双引号所需的包名称。

1. 当要求提供镜像站点，请选择的任何站点，便于在你的位置。

如果目标包依赖于其他包，R 安装程序将自动下载的依赖项，并为你安装它们。

如果你有多个实例的 SQL Server，通过并行实例的 SQL Server 2016 R Services 和 SQL Server 2017 机器学习服务，例如运行单独为每个实例的安装，如果你想要使用两个上下文中的包。 无法在实例之间共享包。

## <a name = "bkmk_offlineInstall"></a> 使用的 R 工具的脱机安装

如果服务器没有 internet 访问，准备包需执行其他步骤。 若要在没有 internet 访问的服务器上安装 R 包，必须：

+ 预先分析依赖关系。
+ 目标包下载到具有 Internet 访问的计算机。
+ 将任何所需的包下载到同一台计算机，并将所有包都放置在单个包存档中。
+ 如果它已不压缩格式的 zip 存档。
+ 将包存档复制到服务器上的位置。
+ 安装目标包指定为源存档文件。

> [!IMPORTANT] 
>  请确保分析所有依赖项并下载**所有**所需的包**之前**开始安装。 我们建议[miniCRAN](https://mran.microsoft.com/package/miniCRAN)此进程。 此 R 包将您想要安装、 分析依赖关系，并且获取所有压缩的文件的包的列表。 miniCRAN 然后创建一个存储库，可以复制到服务器计算机。 有关详细信息，请参阅[创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)

此过程假定您已经准备了你所需的压缩格式，现在即可将其复制到服务器的所有包。

1. 复制包压缩文件，或包含中的所有包的完整存储库的多个包压缩格式，服务器可以访问的位置。

2. 打开服务器上安装该实例的 R 工具的文件夹。 例如，如果使用 SQL Server 2016 R Services 的系统上使用 Windows 命令提示符，切换到`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 右键单击 RGui 或 RTerm 并选择**以管理员身份运行**。

4. 运行 R 命令`install.packages`并指定包或存储库名称和压缩文件的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令中提取 R 包`mynewpackage`从本地 zip 文件，假定已将副本保存在目录中`C:\Temp\Downloaded packages`，并在本地计算机上安装包。 如果包有任何依赖项，安装程序将检查现有包库中。 如果你已创建的存储库，包括依赖项，则安装程序将安装所需的包。

    如果任何所需的包不存在实例库中，无法在压缩文件中找到，目标包的安装将失败。

## <a name="see-also"></a>请参阅

+ [安装新 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)
