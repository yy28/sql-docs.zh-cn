---
title: 在 SQL Server 计算机学习 Services 上安装新的 R 包 |Microsoft 文档
description: 将新的 R 包添加到 SQL Server 2016 R Services 或 SQL Server 自 2017 年 1 机器学习 Services （数据库）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 57c5d4b9c3584a4aa556b1f4b6f7541a14f91a00
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="install-new-r-packages-on-sql-server"></a>在 SQL Server 上安装新的 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何将新的 R 包安装到何处启用机器学习的 SQL Server 的实例。

有多种方法可以安装新的 R 包，具体取决于你拥有 SQL Server 的版本，以及服务器是否具有 internet 访问权限。

+ [安装新包使用 R 工具具有 internet 访问权限](#bkmk_rInstall)

    使用传统的 R 命令从 Internet 安装包。 这是最简单的方法，但需要管理访问权限。

    **适用于：**[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]。 此外所需的实例[!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]通过 Ddl 的包管理尚未启用。

+ [使用的服务器上安装新的 R 包**没有**internet 访问权限](#bkmk_offlineInstall)

    如果服务器没有 internet 访问权限，需要执行一些其他步骤来准备的包。 本部分介绍如何准备所需的包及其依赖项安装文件。

+ [使用创建外部库语句安装包](#bkmk_createlibrary) 

    [创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)语句提供 SQL Server 自 2017 年，以使其可以创建无需运行 R 包库中或直接的 Python 代码。 但是，此方法要求你提前准备所有必需的程序包，并需要附加的数据库的权限。

    **适用于：** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]; 其他限制条件

## <a name="bkmk_rInstall"></a> 安装新的 R 包，使用 Internet

你可以使用标准 R 工具的 SQL Server 2016 或 SQL Server 2017 实例上安装新包。 此过程需要你计算机上的管理员。

> [!IMPORTANT] 
> 请务必将包安装到当前实例相关联的默认库。 永远不会将包安装到用户目录中。

此过程描述如何安装使用 RGui; 包但是，你可以使用 RTerm 或任何其他 R 命令行工具，它支持提升的访问权限。

### <a name="install-a-package-using-rgui-or-rterm"></a>使用 RGui 或 RTerm 安装程序包

1. 导航到安装实例的 R 库的位置的服务器上的文件夹。

  **默认实例**

    SQL Server 自 2017 年 1: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **命名实例**

    SQL Server 自 2017 年 1: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

  如果已使用绑定来升级机器学习组件，则路径可能已更改。 在安装新包之前，始终检查实例路径。 

2. 右键单击 RGui.exe，然后选择**以管理员身份运行**。

    如果你没有所需的权限，请与数据库管理员联系并提供所需的包的列表。

3. 从命令行中，如果您知道包名称中，你可以键入：`install.packages("the_package-name")`双引号所需的包名称。

4. 当系统询问的镜像站点，选择适用于你的位置的任何站点。

5. 如果目标包依赖于其他包，R 安装程序将自动下载依赖项，并为你安装它们。

6. 对于每个实例，你需要使用包，可单独运行安装。 包无法在实例之间共享。

## <a name = "bkmk_offlineInstall"></a> 使用 R 工具的脱机安装

若要在没有 internet 访问的服务器上安装 R 包，你必须：

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

2. 打开其中安装实例的 R 库服务器上的文件夹。 例如，如果使用 Windows 命令提示符，导航到 RTerm.Exe 或 RGui.exe 所在位置的目录。

  **默认实例**

    SQL Server 自 2017 年 1: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **命名实例**

    SQL Server 自 2017 年 1: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. 右键单击 RGui 或命令提示符，然后选择**以管理员身份运行**。

4. 运行 R 命令`install.packages`并指定包或存储库名称和压缩文件的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令将 R 包提取`mynewpackage`从其本地 zip 文件，假定副本保存在目录`C:\Temp\Downloaded packages`，并在本地计算机上安装包。 如果包具有任何依赖关系，安装程序正在检查库中的现有包。 如果你已创建包括依赖项的存储库，则安装程序将安装所需的包。

    如果任何所需的程序包不是实例库中存在，并且无法在压缩文件中找到，目标包的安装将失败。

## <a name="bkmk_createlibrary"></a> 使用 DDL 语句要安装包 

在 SQL Server 自 2017 年，你可以使用[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)语句以将包或组的包添加到特定数据库或实例。 此 DDL 语句和支持的数据库角色旨在促进安装和管理包由数据库所有者无需使用 R 或 Python 工具。

此过程需要一些准备工作，相比安装包使用常规的 R 或 Python 方法。

+ 所有包都必须可用作本地压缩文件，而不是从 internet 下载。

    如果在服务器上没有对文件系统的访问，你还可以传递一个完整的软件包作为变量，使用的二进制格式。 有关详细信息，请参阅[创建外部库](../../t-sql/statements/create-external-library-transact-sql.md)。

+ 如果所需包不可用，则语句将失败。 你必须分析你想要安装并确保包将上载到服务器和数据库的包的依赖关系。 我们建议使用**miniCRAN**或**igraph**用于分析包依赖关系。

+ 你必须在数据库上具有必需的权限。 有关详细信息，请参阅[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

### <a name="prepare-the-packages-in-archive-format"></a>准备存档格式中的包

1. 如果你正在安装单个包，下载 zip 格式中的包。 

2. 如果包需要其他任何包，你必须验证所需的包是否可用。 MiniCRAN 可用于分析目标包并确定其所有依赖项。 

3. 将压缩的文件或包含所有程序包添加到服务器上的本地文件夹的 miniCRAN 存储库的复制。

4. 打开**查询**窗口中，使用具有管理权限的帐户。

5. 运行 T-SQL 语句`CREATE EXTERNAL LIBRARY`将压缩的包集合上传到数据库。

    例如，以下语句名称作为包源 miniCRAN 存储库包含**randomForest**包，以及其依赖项。 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    不能使用的任意名称;外部库名称必须有期望加载或调用包时要使用的相同名称。

6. 如果已成功创建了库，你可以通过调用存储过程内 SQL Server 中运行包。
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    library(randomForest)'
    ```

### <a name="known-issues-with-create-external-library"></a>创建外部库的已知的问题

在这些情况下支持创建外部库：

+ 没有依赖项安装单个包。
+ 要安装包具有依赖项，并已事先准备好所有包。 

如果缺少任何包的依赖项，DDL 语句将失败。 例如，已知安装过程会在这些情况下失败：

+ 安装具有第二层依赖关系的包并不会分析未扩展到第二级别包。 例如，你想要安装**gglot2**，并标识清单中列出的所有包; 但是，这些包具有未安装其他依赖项。
+ 你已安装一组要求不同版本的支持包的包，并且你的服务器具有错误版本。

## <a name="package-installation-tips"></a>包安装提示

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


### <a name="know-which-library-you-are-using-for-installation"></a>了解用于安装的库

如果以前已修改的 R 环境的计算机上，然后才能安装任何内容，暂停一段时间，并确保 R 环境变量`.libPath`使用一个路径。

此路径应指向实例 R_SERVICES 文件夹。 有关详细信息，请参阅[与 SQL Server 安装的 R 包](installing-and-managing-r-packages.md)。

### <a name="side-by-side-installation-with-r-server"></a>使用 R Server 通过并行安装

如果已安装除了 SQL Server 计算机学习 Services 的 Microsoft 机器学习 Server （独立版），则计算机应该具有单独的安装中的 R 对于每个，与所有的 R 工具和库的重复项。

安装到 R_SERVER 库的包只由 Microsoft R Server 和 SQL Server 无法访问。 请务必使用`R_SERVICES`库安装你想要使用 SQL Server 中的包时。

### <a name="how-to-determine-which-packages-are-already-installed"></a>如何确定哪些包已安装？

 请参阅[与 SQL Server 安装的 R 包](installing-and-managing-r-packages.md)