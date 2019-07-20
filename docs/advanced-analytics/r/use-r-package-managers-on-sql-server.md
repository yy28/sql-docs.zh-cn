---
title: 使用 R 包管理器
description: 使用诸如 install 这样的标准 R 命令将新的 R 包添加到 SQL Server 2016 R Services 或 SQL Server 2017 机器学习服务 (数据库内)。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: da14d2f00a6eb0c0ed52a50d27b6f1d06b062cf5
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344869"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>使用 R 包管理器在 SQL Server 上安装 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

你可以使用标准 R 工具在 SQL Server 2016 或 SQL Server 2017 的实例上安装新包, 同时提供计算机具有打开的端口80并拥有管理员权限。

> [!IMPORTANT] 
> 请确保将包安装到与当前实例关联的默认库。 请勿将包安装到用户目录。

此过程使用 Rgui.exe, 但你可以使用 Rterm.exe 或支持提升的访问权限的任何其他 R 命令行工具。

## <a name="install-a-package-using-rgui"></a>使用 Rgui.exe 安装包

1. [确定实例库的位置](../package-management/default-packages.md)。 导航到安装 R 工具的文件夹。 例如, SQL Server 2017 默认实例的默认路径如下所示:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. 右键单击 "Rgui.exe", 然后选择 "以**管理员身份运行**"。 如果没有所需的权限, 请与数据库管理员联系, 并提供所需的包的列表。

1. 在命令行中, 如果知道包名称, 可以键入:`install.packages("the_package-name")`包名称需要双引号。

1. 当系统要求提供镜像站点时, 请选择对你的位置很方便的任何站点。

如果目标包依赖于其他包, R 安装程序会自动下载依赖项并为你安装这些依赖项。

如果你有多个 SQL Server 实例, 如 SQL Server 2016 R Services 的并行实例和 SQL Server 2017 机器学习服务, 若要在这两个上下文中使用该包, 请分别对每个实例运行安装。 不能跨实例共享包。

## <a name = "bkmk_offlineInstall"></a>使用 R 工具进行脱机安装

如果服务器无法访问 internet, 则需要执行其他步骤来准备包。 若要在无法访问 internet 的服务器上安装 R 包, 你必须:

+ 提前分析依赖关系。
+ 将目标包下载到有 Internet 访问权限的计算机。
+ 将所有所需的包下载到相同的计算机, 并将所有包置于单个包存档中。
+ 如果存档尚未打包, 则压缩存档。
+ 将包存档复制到服务器上的某个位置。
+ 安装目标包, 将存档文件指定为源。

> [!IMPORTANT] 
>  在开始安装**之前**, 请确保分析所有依赖项并下载**所有**所需的包。 建议为此过程[miniCRAN](https://mran.microsoft.com/package/miniCRAN) 。 此 R 包获取你要安装的包的列表, 分析依赖关系, 并为你获取所有压缩的文件。 然后, miniCRAN 创建单个存储库, 你可以将其复制到服务器计算机。 有关详细信息, 请参阅[使用 MiniCRAN 创建本地包存储库](create-a-local-package-repository-using-minicran.md)

此过程假定您已准备好所需的所有包, 并采用压缩格式, 并已准备好将它们复制到服务器。

1. 将包的压缩文件或多个包 (包含压缩格式的所有包) 复制到服务器可以访问的位置。

2. 打开服务器上安装了实例的 R 工具的文件夹。 例如, 如果在具有 SQL Server 2016 R Services 的系统上使用 Windows 命令提示符, 请切换到`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 右键单击 "Rgui.exe" 或 "Rterm.exe", 然后选择 "以**管理员身份运行**"。

4. 运行 R 命令`install.packages`并指定包或存储库名称, 以及压缩文件的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令从本地 zip 文件`mynewpackage`中提取 R 包 (假定你已将副本保存在目录`C:\Temp\Downloaded packages`中), 并将包安装在本地计算机上。 如果包有任何依赖项, 则安装程序会检查库中的现有包。 如果你创建了包含依赖项的存储库, 则安装程序也将安装所需的包。

    如果任何所需的包在实例库中不存在, 并且在压缩文件中找不到, 则目标包的安装将失败。

## <a name="see-also"></a>请参阅

+ [安装新 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)
