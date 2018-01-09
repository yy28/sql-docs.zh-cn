---
title: "在 SQL Server 上安装其他 R 包 |Microsoft 文档"
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 2821983b39dcd4c301ea4b49713de0cdd3550a65
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="install-additional-r-packages-on-sql-server"></a>在 SQL Server 上安装其他 R 包

本文介绍如何将新的 R 包安装到何处启用机器学习的 SQL Server 的实例。

**适用范围：** 
+ [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]  [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]
+ [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="prerequisites"></a>必备条件

+ 确定是否存在包的 Windows 版本：[获取正确的包版本和格式](#packageVersion)

+ 如果服务器没有 internet 访问权限，你必须提前下载 Windows 二进制文件：[下载 zip 文件](#bkmk_zipPreparation)

+ 标识包的依赖项。 

    - 如果服务器具有 internet 访问权限，你无需担心依赖项;可以自动安装所有所需的程序包。

    - 如果该服务器将执行**不**具有 internet 访问权限，您必须标识所有依赖项，并以压缩格式，请提前下载所需的包。 执行此操作的简单办法是使用[miniCRAN](create-a-local-package-repository-using-minicran.md)准备使用所有依赖项包的集合。 然后，此存储库可以复制到服务器计算机中。

+ 检查包兼容性。 包应与在 SQL Server 中运行的 R 版本兼容。

    此外，检查是否包 （或它需要的任何包） 包含通过 SQL Server 或策略会阻止的功能。 例如，某些包是不佳不适用于强制写入的 SQL Server 环境。 此类包可能包括访问网络，使用 Java 或其他框架，通常不使用在 SQL Server 环境或需要提升的文件系统访问权限的包的包。

+ 权限

    运行 SQL Server 的计算机对管理访问权限是必需的。

    此外，若要运行在 SQL Server 中，包必须安装在与当前实例相关联的默认库。 有关如何查找默认库的说明，请参阅[与 SQL Server 安装的 R 包](installing-and-managing-r-packages.md)。
    
    如果你是经验丰富的 R 用户，你可能会习惯于从命令行无需特殊权限，或不带提前进行下载安装包。 但是，此方法在 SQL Server 中不起作用。 在许多情况下 SQL Server 计算机没有 internet 连接。 此外，访问服务器文件或外部存储可能受到限制。 包安装到用户库不能由 SQL Server 中的 R 作业 runnign 访问。 

    如果你没有管理访问权限的 SQL Server 计算机，找到的数据库管理员联系，以帮助包安装。

+ 对于每个实例，你需要使用包，可单独运行安装。

     包无法在实例之间共享。 你可以使用相同的压缩的文件源安装程序包后，独立实例，但包的单独副本添加到每个实例库。

## <a name="install-packages"></a>安装包

本部分提供有关以下方案的包安装步骤：

+ [在具有 Internet 访问的服务器上安装新的包](#bkmk_rInstall)
+ [使用的服务器上执行包的脱机安装**没有**internet 访问权限](#bkmk_offlineInstall)
+ [将包安装到使用 RevoScaleR 的 SQL Server 计算上下文](#bkmk_rAddPackage)
+ [使用创建外部库语句安装包](#bkmk_createlibrary)（SQL Server 2017; 其他应用的限制）

### <a name="bkmk_rInstall"></a>使用 R 工具的联机安装

你可以使用标准 R 工具的 SQL Server 2016 或 SQL Server 2017 实例上安装新包。 但是，您必须是管理员才能这样做。

1.  导航到安装实例的 R 库的位置的服务器上的文件夹。

    > [!IMPORTANT] 
    > 请务必将包安装到当前实例相关联的默认库。 永远不会将包安装到用户目录中。

    如果你没有所需的权限，请与数据库管理员联系并提供所需的包的列表。

2.  以管理员身份打开 R 命令提示符。

    例如，如果使用 Windows 命令提示符，导航到 RTerm.Exe 或 RGui.exe 所在位置的目录。 

    **默认实例**

    SQL Server 自 2017 年 1:`C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **命名实例**

    SQL Server 自 2017 年 1:`C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

    如果已使用绑定来升级机器学习组件，则路径可能已更改。 在安装新包之前，始终检查实例路径。 

3.  运行 R 命令`install.packages`安装该包。 例如，以下语句会将常用 e1071 包安装。 

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    两个双引号所需的包名称。

4. 当系统询问的镜像站点，选择适用于你的位置的任何站点。

5. 如果目标包依赖于其他包，R 安装程序将自动下载依赖项，并为你安装它们。

> [!IMPORTANT]
> 对于每个实例，你需要使用包，可单独运行安装。 包无法在实例之间共享。

### <a name = "bkmk_offlineInstall"></a>使用 R 工具的脱机安装 

如果你想要安装的包具有依赖关系，准备**所有**所需提前的包。  请参阅[安装提示](#bkmk_tips)部分有关准备包的帮助。

> [!IMPORTANT]
>  每当你在没有 internet 访问的服务器上安装包，很重要，请提前分析完成的依赖关系，请确保你已下载了所有必需的程序包**之前**开始安装。 我们建议[miniCRAN](https://mran.microsoft.com/package/miniCRAN)此进程。 此 R 包将你想要安装、 分析依赖项，并为你获取所需的所有压缩的文件的包的列表。 miniCRAN 然后创建到单个存储库，可以将其复制到服务器计算机。
> 
> 有关详细信息，请参阅[创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)

1. 将压缩格式存储库或包复制到本地共享或在服务器可以访问其他位置中。

2.  找到其中安装实例的 R 库服务器上的文件夹。

    例如，如果使用 Windows 命令提示符，导航到 RTerm.Exe 或 RGui.exe 所在位置的目录。

    **默认实例**

    SQL Server 自 2017 年 1:`C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **命名实例**

    SQL Server 自 2017 年 1:`C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. 以管理员身份打开 R 命令提示符。

4.  运行 R 命令`install.packages`并指定包或存储库名称和压缩文件的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令将 R 包提取`mynewpackage`从其本地 zip 文件，假定副本保存在目录`C:\Temp\Downloaded packages`，并在本地计算机上安装包。 如果包具有任何依赖关系，安装程序正在检查库中的现有包。 如果已创建包括依赖项的存储库，则安装程序将安装的 requireed 包。

    如果任何所需的程序包不是实例库中存在，并且无法在压缩文件中找到，目标包的安装将失败。

### <a name="bkmk_rAddPackage"></a>从远程 R 客户端的服务器上安装 R 包

最新版本中[R 服务器或计算机学习服务器](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server)，RevoScaleR 包括支持将新的 R 包安装到 SQL Server 计算上下文的函数。 

1. 在开始之前，确保满足这些条件：

    + 客户端具有 RevoScale 9.0.1 或更高版本。
    + SQL Server 实例上已安装的 RevoScaleR 为相应的版本。
    + [包管理功能](..\r\r-package-how-to-enable-or-disable.md)实例上已启用。
    + 现在允许你在上的指定的实例和 ddatabase 安装中共享的包或 prvate 上下文中，数据库角色的成员。

2. 从 R 的命令行，定义连接字符串的实例和数据库，并使用的连接字符串具有[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)构造函数来创建 SQL Server 计算上下文。

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. 创建你想要安装并将该列表保存在一个字符串变量中的包的列表。

    ```R
    packageList <- c("e1071", "mice")
    ```

4. 调用[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)并传递计算上下文和包含包名称的字符串变量。

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    如果从属包是必需的它们会同时安装，假设 internet 连接不可用。
    
    在此示例中，因为未指定的所有者和作用域，未安装程序包使用该用户的默认作用域中建立的连接，用户的凭据。

### <a name="bkmk_createlibrary"></a>使用 miniCRAN 存储库和创建外部库来安装包 

SQL Server 2017 提供用于安装和管理使用 T-SQL 的 R 包的新功能。 但是，此过程需要，包可根据本地压缩文件，而不是从 internet 下载。 如果不事先准备的所有包，则语句将失败。

在这些情况下支持创建外部库：

+ 你没有依赖项安装单个包
+ 依赖项而安装多个包，并且已提前准备好所有包。 

**步骤**

1.  准备 zip 格式中的包或创建包含包和其依赖项 miniCRAN 存储库。  

2. 将压缩的文件或存储库复制到服务器上的本地文件夹中。

     > [!IMPORTANT]
     > 你指定为源必须包含目标包，以及任何相关的所需的包文件。

3. 作为管理员，运行 T-SQL 语句`CREATE EXTERNAL LIBRARY`将压缩的包集合上传到数据库。

    例如，以下语句引用包含 randomForest 包和其依赖项 miniCRAN 存储库。 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    不能使用的任意名称中创建的语句;外部库名称必须有期望加载或调用包时要使用的相同名称。

4. 通过运行存储过程内的代码与 SQL Server 安装或多个包使用。
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    如果成功，**消息**窗口应报告一条消息，如"包 randomForest 已成功解压缩和 MD5 总和检查"和"已完成链接执行"。

    如果安装失败，所有包都失败安装，并且后续尝试安装包安装可能还会都失败，与此消息： 

    "错误 rxSqlPkgInstallPackages 中...无法安装包-请检查日志以了解详细信息"

## <a name="package-installation-tips-and-frequently-asked-questions-faq"></a>包安装提示和常见问题 (FAQ)

本部分提供各种的提示和与 SQL Server 上的 R 包安装相关的常见问题。

###  <a name="packageVersion"></a>获取正确的包版本和格式

可以从多个来源获取 R 包，最广为人知的是 CRAN 和 Bioconductor。 R 语言的官方站点 (<https://www.r-project.org/>) 列出了许多这样的资源。 很多包发布到 GitHub，从何处可以获取源代码。 但是，您可能提供了通过你的公司中的某个人开发的 R 包。

而不考虑源，必须确保你想要安装的程序包具有适用于 Windows 平台的二进制格式。 否则，无法在 SQL Server 环境中运行下载的包。

### <a name="bkmk_zipPreparation"></a>下载包为压缩文件

如果没有 internet 连接的服务器上的安装，必须下载脱机安装的压缩文件的格式中的包的副本。 请不要解压缩包。

例如，下面的过程描述现在，若要获取的正确版本[FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) bioconductor，假定计算机具有 internet 访问权限的包。

1.  在“包存档”列表中，查找“Windows 二进制文件”版本。

2.  右键单击的链接。ZIP 文件，并选择**目标另存为**。

3.  导航到本地文件夹，zip 的包存储中，然后单击**保存**。

    此过程将创建包的本地副本。 如果你收到下载错误，请尝试不同的镜像站点。

4. 已下载包存档后，你可以安装包，或将压缩的包复制到没有 internet 访问的服务器。

> [!TIP]
> 如果错误地安装而不是下载二进制文件的包，下载的压缩文件的副本还会保存到你的计算机。 为包已安装，以确定文件位置，请观看的状态消息。 可以将该 zip 的文件复制到没有 internet 访问的服务器。
> 如果下载包使用此方法时，将不包括包的依赖项。 

有关的 zip 文件格式，以及如何创建 R 包内容的详细信息，我们建议本教程中，你可以从 R 项目站点的 PDF 格式下载该：[创建 R 包](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)。

### <a name="bkmk_packageDependencies"></a>获取包的依赖项

R 包经常依赖于多个其他包，其中一些可能不可用的实例所使用的默认 R 库中。 有时包需要已安装的从属包的不同版本。

如果你需要安装多个包，或想要确保你的组织中的每个人都获得正确的包类型和版本，我们建议你使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)该包，以创建可共享的本地存储库在多个用户或计算机。 有关详细信息，请参阅[创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

### <a name="permissions"></a>权限

本部分介绍的不同级别的权限所需的安装 SQL Server 2016 和 SQL Server 自 2017 年中的包。 可以安装使用 R 工具或 SQL Server，但略有不同的进程和权限。

-   SQL Server 2016

    在此版本中，仅计算机上的管理员可以安装包，到所需的位置。 使用标准 R 工具来安装包，但你必须以管理员身份运行，并使用与实例关联的 R 工具。

-   SQL Server 2017

    如果具有管理访问权限，你可以通过使用 R 工具在实例范围内安装包。

    如果你是数据库的所有者，你可以从远程客户端，安装 R 包，如果定义了一个连接并连接到使用 RxInSqlServer 的实例。
    
    此版本包含可在即将发布的版本中支持的数据库管理员的 R 或 Python 包管理的新功能。 若要使用此功能，数据库管理员必须首先启用基于每个实例的程序包管理功能。 启用此功能后，单个用户可以安装到特定的数据库，具体取决于其数据库角色的包。 有关详细信息，请参阅[启用或禁用对 SQL Server 的 R 包管理](../r/r-package-how-to-enable-or-disable.md)。

> [!IMPORTANT]
> 
> 有经验的 R 用户习惯于在用户库中，安装包和作为一部分 R 解决方案，然后引用该文件夹中的包，通过指定的文件路径。 但是，在 SQL Server 中不支持这种做法。 有关详细信息和解决方法，请参阅[如何使用用户库中的包](packages-installed-in-user-libraries.md)。

### <a name="establish-a-single-mirror-site-as-standard"></a>作为标准建立一个镜像站点

为了避免每次添加新包都必须选择镜像站点，可将 R 开发环境配置为始终使用相同的存储库。 若要执行此操作，编辑全局 R 设置文件， **。Rprofile**，并添加以下行：

`options(repos=structure(c(CRAN="<mirror site URL>")))`

上列出需当前 CRAN 镜像[此站点](https://cran.r-project.org/mirrors.html)。

有关首选项以及 R 运行时启动时加载的其他文件的详细信息，请从 R 控制台运行此命令：`?Startup`

### <a name="know-which-library-you-are-using-for-installation"></a>了解用于安装的库

如果以前已修改的 R 环境的计算机上，然后才能安装任何内容，暂停一段时间，并确保 R 环境变量`.libPath`使用一个路径。

此路径应指向实例 R_SERVICES 文件夹。 有关详细信息，请参阅[与 SQL Server 安装的 R 包](installing-and-managing-r-packages.md)。

### <a name="side-by-side-installation-with-r-server"></a>使用 R Server 通过并行安装

如果已安装除了 SQL Server 计算机学习 Services 的 Microsoft 机器学习 Server （独立版），则计算机应该具有单独的安装中的 R 对于每个，与所有的 R 工具和库的重复项。

> [!IMPORTANT]
> 
> 安装到 R_SERVER 库的包只由 Microsoft R Server 和 SQL Server 无法访问。
> 
> 请务必使用`R_SERVICES`库安装你想要使用 SQL Server 中的包时。

### <a name="how-to-determine-which-packages-are-already-installed"></a>如何确定哪些包已安装？

 请参阅[与 SQL Server 安装的 R 包](installing-and-managing-r-packages.md)