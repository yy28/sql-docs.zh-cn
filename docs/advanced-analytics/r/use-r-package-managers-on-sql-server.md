---
title: 使用 R 包管理器
description: 使用标准 R 命令（如 install.packages）将新的 R 包添加到 SQL Server 2016 R Services 或 SQL Server 机器学习服务（数据库内）。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f6d828a7267ab2b4b1def17f9d1c6bf4a6018dc
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69633617"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>使用 R 包管理器在 SQL Server 上安装 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

可以使用标准 R 工具在 SQL Server 2016 或 SQL Server 2017 实例上安装新包，前提是计算机具有打开的端口 80，并且你拥有管理员权限。

> [!IMPORTANT] 
> 请确保将包安装到与当前实例关联的默认库。 请勿将包安装到用户目录。

此过程使用 RGui，但你可以使用 RTerm 或任何其他支持提升的访问权限的 R 命令行工具。

## <a name="install-a-package-using-rgui"></a>使用 RGui 安装包

1. [确定实例库的位置](../package-management/r-package-information.md)。 导航到安装 R 工具的文件夹。 例如，SQL Server 2017 默认实例的默认路径如下所示：`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. 右键单击 RGui.exe，然后选择“以管理员身份运行”  。 如果没有所需的权限，请与数据库管理员联系以获取所需包的列表。

1. 在命令行中，如果知道包名称，则可以键入：`install.packages("the_package-name")` 包名称需要使用双引号。

1. 要求提供镜像站点时，请选择适合位置的任何站点。

如果目标包依赖于其他包，R 安装程序会自动下载并安装这些包。

在具有多个 SQL Server 实例（如 SQL Server 2016 R Services 和 SQL Server 机器学习服务的并行实例）情况下，如果要在这两个上下文中使用包，请为每个实例单独运行安装。 无法跨实例共享包。

## <a name = "bkmk_offlineInstall"></a> 使用 R 工具进行脱机安装

如果服务器无法访问 Internet，则需要执行其他步骤来准备包。 要在无法访问 Internet 的服务器上安装 R 包，你必须：

+ 提前分析依赖关系。
+ 将目标包下载到具有 Internet 访问权限的计算机。
+ 将所有所需的包下载到同一计算机，并将所有包置于单个包存档中。
+ 如果尚未压缩存档，则将其压缩。
+ 将包存档复制到服务器上的某个位置。
+ 安装目标包，将存档文件指定为源。

> [!IMPORTANT] 
>  在开始安装前，请务必分析所有依赖项并下载所有所需的包   。 建议在此过程中使用 [miniCRAN](https://mran.microsoft.com/package/miniCRAN)。 此 R 包具有要安装的包列表，可分析依赖项，并生成所有压缩文件。 然后，miniCRAN 将创建单个存储库，可以将其复制到服务器计算机。 有关详细信息，请参阅[使用 miniCRAN 创建本地包存储库](create-a-local-package-repository-using-minicran.md)

此过程假定已准备好所需的所有包（压缩格式），并已准备好将它们复制到服务器。

1. 将包压缩文件或包含压缩格式的所有包的完整存储库（如果为多个包）复制到服务器可访问位置。

2. 在安装用于实例的 R 工具的服务上打开文件夹。 例如，如果在具有 SQL Server 2016 R Services 的系统上使用 Windows 命令提示符，请切换到 `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 右键单击 RGui 或 RTerm 并选择“以管理员身份运行”  。

4. 运行 R 命令 `install.packages`，并指定包或存储库名称以及压缩文件的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    该命令从本地压缩文件中提取 R 包 `mynewpackage`（假定已将副本保存在目录 `C:\Temp\Downloaded packages` 中），并将该包安装在本地计算机上。 如果包具有任何依赖项，则安装程序会检查库中的现有包。 如果已创建包含依赖项的存储库，则安装程序还将安装所需的包。

    如果实例库中不存在任何所需的包，并且在压缩文件中找不到这些包，则目标包安装失败。

## <a name="see-also"></a>另请参阅

+ [安装新 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)
