---
title: 在 SQL Server 计算机学习 Services 上安装新的 R 包 |Microsoft 文档
description: 将新的 R 包添加到 SQL Server 2016 R Services 或 SQL Server 自 2017 年 1 机器学习 Services （数据库）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 20ef7181c5ab8c0494f73b205dddcdf1ac0a620e
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
---
# <a name="install-new-r-packages-on-sql-server"></a>在 SQL Server 上安装新的 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何将新的 R 包安装到何处启用机器学习的 SQL Server 的实例。 有多种方法可以安装新的 R 包，具体取决于你拥有 SQL Server 的版本，以及服务器是否具有 internet 连接。 采用以下方法来新包安装是可能的。

| 方法                           | 权限  | 远程/本地 |
|------------------------------------|---------------------------|-------|
| [使用传统的 R 包管理器](#bkmk_rInstall)  | 管理员 | Local |
| [使用 RevoScaleR](use-revoscaler-to-manage-r-packages.md) | 管理员 | Local |
| [使用 T-SQL （创建外部库）](install-r-packages-tsql.md) | 安装程序，之后数据库角色的管理员 | both 
| [使用 miniCRAN 创建本地存储库](create-a-local-package-repository-using-minicran.md) | 安装程序，之后数据库角色的管理员 | both |

## <a name="bkmk_rInstall"></a> 安装 R 包通过 Internet 连接

你可以使用标准 R 工具的 SQL Server 2016 实例上安装新包或 SQL Server 2017，提供在计算机已打开端口 80 并且你具有管理员权限。

> [!IMPORTANT] 
> 请务必将包安装到当前实例相关联的默认库。 永远不会将包安装到用户目录中。

此过程使用 RGui，但是你可以使用 RTerm 或任何其他 R 命令行工具，它支持提升的访问权限。

### <a name="install-a-package-using-rgui"></a>使用 RGui 安装程序包

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
> > 请确保分析所有依赖项，并下载**所有**所需包**之前**开始安装。 我们建议[miniCRAN](https://mran.microsoft.com/package/miniCRAN)此进程。 此 R 包将你想要安装、 分析依赖项，并为你获取所需的所有压缩的文件的包的列表。 miniCRAN 然后创建到单个存储库，可以将其复制到服务器计算机。
> 
> 有关详细信息，请参阅[创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)

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

## <a name="tips-for-package-installation"></a>包安装的提示

本部分提供各种的提示和与 SQL Server 上的 R 包安装相关的常见问题。

###  <a name="packageVersion"></a> 获取正确的包版本和格式

有多个来源获取 R 包，例如 CRAN 和 Bioconductor。 R 语言官方站点 (<https://www.r-project.org/>) 列出了很多这些资源。 很多包发布到 GitHub，从何处可以获取源代码。 最后，您可能提供了通过你的公司中的某个人开发的 R 包，或您具有您编写的自定义包。

而不考虑源，然后再尝试安装包，确保你获取 Windows 平台的二进制格式。 

### <a name="bkmk_zipPreparation"></a> 下载包为压缩文件

如果没有 internet 连接的服务器上的安装，必须下载脱机安装的压缩文件的格式中的包的副本。 **请不要解压缩包。**

例如，下面的过程描述现在，若要获取的正确版本[FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) bioconductor，假定计算机具有 internet 访问权限的包。

1.  在“包存档”列表中，查找“Windows 二进制文件”版本。

2.  右键单击的链接。ZIP 文件，并选择**目标另存为**。

3.  导航到本地文件夹，zip 的包存储中，然后单击**保存**。

    此过程将创建包的本地副本。 

4. 如果你收到下载错误，请尝试不同的镜像站点。

5. 已下载包存档后，你可以安装包，或将压缩的包复制到没有 internet 访问的服务器。

> [!TIP]
> 如果错误地安装而不是下载二进制文件的包，下载的压缩文件的副本还会保存到你的计算机。 为包已安装，以确定文件位置，请观看的状态消息。 可以将该 zip 的文件复制到没有 internet 访问的服务器。
> 
> 但是，当你获得包使用此方法时，将不包括依赖关系。 

### <a name="bkmk_packageDependencies"></a> 获取所需的程序包

R 包经常依赖于多个其他包，其中一些可能不可用的实例所使用的默认 R 库中。 有时包需要已安装的从属包的不同版本。

如果你需要安装多个包，或想要确保你的组织中的每个人都获得正确的包类型和版本，我们建议你使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)包以分析完成的依赖关系链。 minicRAN 创建可以在多个用户或计算机之间共享的本地存储库。 有关详细信息，请参阅[创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。


### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>知道要安装到的库和已安装的包。

如果以前已修改的 R 环境的计算机上，然后才能安装任何内容，暂停一段时间，并确保 R 环境变量`.libPath`使用一个路径。

此路径应指向实例 R_SERVICES 文件夹。 有关详细信息，包括如何确定哪些包已安装，请参阅[与 SQL Server 安装的 R 包](installing-and-managing-r-packages.md)。

### <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>与独立 R 或 Python 服务器通过并行安装

如果你安装 SQL Server 自 2017 年 1 Microsoft 机器学习 Server （独立） 或 SQL Server 2016 R Server （独立） 除了数据库中分析 （SQL Server 自 2017 年 1 机器学习服务和 SQL Server 2016 R Services），你的计算机拥有分隔为每个包含重复项的所有 R 工具和库的 R 安装。

这些包安装到 R_SERVER 库只由独立服务器，并且不由 SQL Server （数据库） 实例访问。 始终使用`R_SERVICES`库安装你想要使用 SQL Server 上的数据库中的包时。
