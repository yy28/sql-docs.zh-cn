---
title: 在 SQL Server 计算机学习 Services 上安装新的 R 包 |Microsoft 文档
description: 将新的 R 包添加到 SQL Server 2016 R Services 或 SQL Server 自 2017 年 1 机器学习 Services （数据库）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8f7b0ee2b623f6a208a92823948bf0295bae33f6
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707495"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>使用 R 包管理器在 SQL Server 上安装 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

你可以使用标准 R 工具的 SQL Server 2016 实例上安装新包或 SQL Server 2017，提供在计算机已打开端口 80 并且你具有管理员权限。

> [!IMPORTANT] 
> 请务必将包安装到当前实例相关联的默认库。 永远不会将包安装到用户目录中。

此过程使用 RGui，但是你可以使用 RTerm 或任何其他 R 命令行工具，它支持提升的访问权限。

## <a name="install-a-package-using-rgui"></a>使用 RGui 安装程序包

1. [确定实例库的位置](installing-and-managing-r-packages.md)。 导航到其中安装 R 工具的文件夹。 例如，SQL Server 2017 默认实例的默认路径如下所示： `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. 右键单击 RGui.exe，然后选择**以管理员身份运行**。 如果你没有所需的权限，请与数据库管理员联系并提供所需的包的列表。

1. 从命令行中，如果您知道包名称中，你可以键入：`install.packages("the_package-name")`双引号所需的包名称。

1. 当系统询问的镜像站点，选择适用于你的位置的任何站点。

如果目标包依赖于其他包，R 安装程序将自动下载依赖项，并为你安装它们。

如果你有多个实例的 SQL Server，如通过并行实例的 SQL Server 2016 R Services 和 SQL Server 自 2017 年 1 机器学习 Services，运行单独为每个实例的安装，如果你想要使用两个上下文中的包。 包无法在实例之间共享。

## <a name = "bkmk_offlineInstall"></a> 使用 R 工具的脱机安装

如果服务器没有 internet 访问权限，需要其他步骤来准备的包。 若要在没有 internet 访问的服务器上安装 R 包，你必须：

+ 提前分析依赖关系。
+ 目标包下载到具有 Internet 访问的计算机。
+ 将任何所需的程序包下载到同一台计算机，并将所有程序包都放在单个包存档。
+ 如果它尚不压缩格式，则 zip 存档。
+ 将包存档复制到服务器上的位置。
+ 安装为源指定存档文件的目标包。

> [!IMPORTANT] 
>  请确保分析所有依赖项，并下载**所有**所需包**之前**开始安装。 我们建议[miniCRAN](https://mran.microsoft.com/package/miniCRAN)此进程。 此 R 包将你想要安装、 分析依赖项，并为你获取所需的所有压缩的文件的包的列表。 miniCRAN 然后创建到单个存储库，可以将其复制到服务器计算机。 有关详细信息，请参阅[创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)

此过程假定你已准备好，需要以压缩格式的虚拟机和模板，就可以将它们复制到服务器的所有包。

1. 复制包压缩文件，或对于多个包，包含中的所有程序包的完整存储库压缩格式，服务器可以访问的位置。

2. 打开其中安装 R 工具的实例的服务器上的文件夹。 例如，如果使用的具有 SQL Server 2016 R Services 的系统上的 Windows 命令提示符下，切换到`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 右键单击 RGui 或 RTerm 并选择**以管理员身份运行**。

4. 运行 R 命令`install.packages`并指定包或存储库名称和压缩文件的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令将 R 包提取`mynewpackage`从其本地 zip 文件，假定副本保存在目录`C:\Temp\Downloaded packages`，并在本地计算机上安装包。 如果包具有任何依赖关系，安装程序正在检查库中的现有包。 如果你已创建包括依赖项的存储库，则安装程序将安装所需的包。

    如果任何所需的程序包不是实例库中存在，并且无法在压缩文件中找到，目标包的安装将失败。

## <a name="see-also"></a>另请参阅

+ [安装新 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)