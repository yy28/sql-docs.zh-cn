---
title: "在 SQL Server 上安装其他 R 包 |Microsoft 文档"
ms.date: 11/15/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: f8d20c5b5b687a6d9d94cd97605f294cead27215
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="install-additional-r-packages-on-sql-server"></a>在 SQL Server 上安装其他 R 包

本文介绍如何将新的 R 包安装到何处启用机器学习的 SQL Server 的实例。

> [!IMPORTANT]
> 添加新的程序包的过程取决于 SQL Server 正在运行和你使用的工具的版本。 

**适用于：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]和  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]
[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="overview-of-package-installation-process"></a>包安装过程的概述

1.  确定是否存在包的 Windows 版本：[获取正确的包版本和格式](#packageVersion)

2.  如果服务器没有 internet 访问权限，请提前下载二进制文件：[下载 zip 文件](#bkmk_zipPreparation)

    请务必检查包依赖关系并获取任何相关的包可能需要在安装过程。 若要准备包和其依赖项的集合，我们建议[miniCRAN 包](#bkmk_packageDependencies)。

    如果出现下载或安装错误，请尝试不同的镜像站点。

3.  安装包的方式取决于是否在服务器具有 internet 访问权限，并在你的 SQL Server 版本上。 建议的流程如下所示：

    **SQL Server 2016 的软件包安装**
    
    1. 数据科学家提供项目或团队所需的程序包。 使用[miniCRAN](create-a-local-package-repository-using-minicran.md)准备具有它们的依赖项的程序包的集合。

    2. 数据库管理员将包安装到使用 R 工具的实例库。

    **SQL Server 自 2017 年的软件包安装**

    1. 数据库管理员可支持的实例上的包管理，并将用户添加到新的包管理角色。

    2. 数据科学家提供项目或团队所需的程序包。 使用[miniCRAN](create-a-local-package-repository-using-minicran.md)准备具有它们的依赖项的程序包的集合。

    3. 包上载到 SQL Server 实例，使用创建外部库语句。
    
    4. 具有适当权限的任何用户包已添加到实例后，可以将包安装到 R 脚本运行其中，可以通过调用从 R 代码的数据库`sp_execute_external_script`。
    
    5. 具有适当权限的用户也可以安装或从远程 R 客户端，用于程序包管理使用新 RevoScaleR 函数查找包。

## <a name="install-new-packages"></a>安装新的包

本部分提供了用于密钥包安装方案的详细的过程。 选择最佳的方法，具体取决于：

- 你使用的 SQL Server 的版本

- 是否是唯一的实例，所有者，或尝试为使用数据库角色的多人管理包。

- 具有依赖项安装的一个包中或多个包

**使用 SQL Server 包管理**

如果你的实例支持程序包管理功能，你可以使用 T-SQL 或传统的 R 工具。

-  已启用到管理包和基于角色的包访问的位置的 SQL Server 的上载 R 程序包。 用户然后安装使用 T-SQL 的包。

    [使用创建外部库安装包](#bkmk_sqlInstall)

- 使用远程 R 客户端向服务器添加新的包。 需要 SQL Server 自 2017 年。 必须在服务器上启用包管理。 

    [使用 R 时启用包管理的服务器上安装包](#bkmk_rAddPackage)

- 准备用于创建的外部库包含多个包以及其依赖项包库。

    [从 miniCRAN 存储库安装多个程序包](#bkmk_minicran)

**使用传统的 R 工具**

如果你使用的 SQL Server R services 的早期版本，请按照这些说明使用传统的 R 工具安装包。 （可选） 使用 miniCRAN 要准备进行安装的包的集合。

-  将 R 包安装到默认实例库使用 R 工具。 需要管理访问权限。

    [在使用 R 工具的实例库中安装包](#bkmk_rInstall)

- 创建包，以便支持多个包和其依赖项的简单安装共享的的集合。

    [创建使用 miniCRAN 程序包存储库](create-a-local-package-repository-using-minicran.md)

### <a name="bkmk_sqlInstall"></a>使用 SQL Server 工具安装包

1. 确保已在实例上启用了 SQL Server 自 2017 年中的外部库管理功能。

    [如何启用或禁用包管理](r-package-how-to-enable-or-disable.md)

2. 连接到服务器使用具有安装新包，使用本主题中所述的受支持的数据库角色之一的权限的帐户： [for SQL Server 的 R 包管理](r-package-management-for-sql-server-r-services.md)

3.  将压缩的文件包含你想要将安装到的文件夹的服务器计算机上，例如的 R 程序包复制你**用户**或**文档**文件夹。 从网络驱动器或客户端计算机上的文件夹，无法添加包。 如果已使用 miniCRAN 来创建的程序包存储库，将程序包存储库整个复制到任何服务器上的本地文件夹： 即不在网络驱动器上。

    如果你没有访问服务器上的任何文件夹，你可以采用二进制格式传递的包内容。 请参阅[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)有关示例。

4.  从你想要使用的包的数据库，运行[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)语句。

    对于此示例中，我们假定你的帐户有权将新包上载到服务器并安装到**共享**数据库中的作用域。

    以下语句将添加的发行版[zoo](https://cran.r-project.org/web/packages/zoo/index.html)到当前数据库上下文中，从本地文件共享的包。

    ```SQL
    CREATE EXTERNAL LIBRARY zoo
    FROM (CONTENT = 'C:\Temp\RPackages\zoo_1.8-0.zip')
    WITH (LANGUAGE = 'R');
    ```

    如果你使用的数据库所有者 （dbo 角色的成员） 的帐户进行连接，包中可**共享**作用域： 即，它可以安装的任何用户都是成员的`rpkgs-users`角色。

    如果上载使用仅可以访问的帐户的包**私有**作用域，可以仅由你安装包。

4.  若要将程序包安装到的实例使用的默认 R 库，运行 R`library()`内存储的过程 sp_execute_external_script 命令。

    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # load the binaries in zoo
    library(zoo)'
    ```

    如果成功，**消息**窗口应报告一条消息，如"包 zoo 已成功解压缩和 MD5 总和检查"。 如果已安装所需的程序包，则安装进程然后附加并加载所需的程序包。

    > [!NOTE]
    > 未提供所需的程序包时，返回错误:"没有调用程序包\<required_package\>"。 
    > 
    > 若要避免错误，我们建议你事先，检查包依赖关系，或使用 miniCRAN 来收集在运行前一个压缩文件的所有必需的程序包`CREATE EXTERNAL LIBRARY`。

### <a name="bkmk_rAddPackage"></a>使用 R 时启用包管理的服务器上安装包

如果你已启用的实例上的管理包，你可以从使用 RevoScaleR 函数用于程序包管理的远程 R 客户端安装新的 R 包。

1. 在开始之前，确保满足这些条件：

    + 使用最新版本的 Microsoft R 客户端，其中包含对 RevoScale 的更新。
    + 管理包已启用，该实例和数据库。
    + 具有对数据库管理角色之一的权限。

2. 列出你想要安装的字符串变量中的包。

    ```R
    packageList <- c("e1071")
    ```
    
3. 定义连接字符串的实例和数据库管理包在何处启用，并使用连接字符串创建的 SQL Server 计算上下文。

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

4. 调用`rxInstallPackages`并传递计算上下文和包含包名称的字符串变量。

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    如果从属包是必需的它们也将会下载。
    
    在此示例中，因为未指定的包所有者和作用域，使用的凭据进行连接、 用户安装此包，并使用该用户的默认作用域安装包。

### <a name="bkmk_rInstall"></a>在使用 R 工具的实例库中安装包

R 工具可用于在 SQL Server 2016 和 SQL Server 2017 上安装新包。 但是，您必须是管理员才能这样做。

1.  如果服务器没有 internet 访问权限，下载提前包。

    我们建议你使用的程序包存储库准备脱机包的集合。 有关详细信息，请参阅[创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

2.  导航到安装实例的 R 库的位置的服务器上的文件夹。

    > [!IMPORTANT] 
    > 请务必将包安装到当前实例相关联的默认库。 永远不会将包安装到用户目录中。 有关如何查找默认库的说明，请参阅[与 SQL Server 安装的 R 包](installing-and-managing-r-packages.md)。

    对于每个实例，其中运行包，安装包的单独副本。 包无法在实例之间共享。

4.  以管理员身份打开 R 命令提示符。

    例如，如果使用 Windows 命令提示符，导航到 RTerm.Exe 或 RGui.exe 文件所在的目录。 

    **默认实例**

    SQL Server 自 2017 年 1:`C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **命名实例**

    SQL Server 自 2017 年 1:`C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

5.  运行 R 命令`install.packages`安装该包。

    语法取决于是否得到包从 Internet 还是从本地 zip 文件。 

    **安装包使用 internet 连接**

    例如，以下语句会将常用 e1071 包安装。 两个双引号并总是必需的包名称。

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    当系统询问的镜像站点，选择适用于你的位置的任何站点。

    如果目标包依赖于其他包，R 安装程序将自动下载依赖项，并为你安装它们。

    **包手动安装或的计算机上没有 Internet 访问权限**

    如果你要安装的包具有依赖项，请提前获取所需的包并将它们添加到包含其他包压缩文件的文件夹中。 请参阅[安装提示](#bkmk_tips)部分有关准备包的帮助。

    在 R 命令提示符下键入以下命令，以指定要安装的包的路径和名称：

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令从其本地 zip 文件，假定副本保存在目录中提取单个的 R 包`C:\Temp\Downloaded packages`，并将 （包括其依赖项） 的包安装到本地计算机上的 R 库。

### <a name="bkmk_minicran"></a>从 miniCRAN 存储库安装多个程序包

从 miniCRAN 存储库安装包的整个过程是类似于从单个 zip 文件安装的包。 但是，而不是上载 zip 格式中的单个包，miniCRAN 储存库中包含目标包，以及任何相关的所需的包。

1.  准备 miniCRAN 存储库，然后将 zip 的文件复制到服务器上的本地文件夹。

2.  如果使用 T-SQL 的管理员后运行 T-SQL 语句`CREATE EXTERNAL LIBRARY`将压缩的包集合上传到数据库。

    例如，以下语句引用包含 randomForest 包和其依赖项 miniCRAN 存储库。

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

3. 若要使用 SQL Server 安装使用的包，请在存储过程中的 R 代码的一部分运行以下命令。
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    如果成功，**消息**窗口应报告一条消息，如"包 randomForest 已成功解压缩和 MD5 总和检查"和"已完成链接执行"。

## <a name="package-installation-tips"></a>包安装提示

本部分提供各种的提示和与 SQL Server 上的 R 包安装相关的示例代码。 

###  <a name="packageVersion"></a>获取正确的包版本和格式

可以从多个来源获取 R 包，最广为人知的是 CRAN 和 Bioconductor。 R 语言的官方站点 (<https://www.r-project.org/>) 列出了许多这样的资源。 很多包发布到 GitHub，从何处可以获取源代码。 但是，您可能提供了通过你的公司中的某个人开发的 R 包。

而不考虑源，必须确保你想要安装的程序包具有适用于 Windows 平台的二进制格式。 否则，无法在 SQL Server 环境中运行下载的包。

在下载之前，你还应检查包是否与在 SQL Server 中运行的 R 版本兼容。

### <a name="bkmk_zipPreparation"></a>下载包为压缩文件

在没有 internet 访问权限的服务器上的安装，下载脱机安装的压缩文件的格式中的包的副本。 请不要解压缩包。

例如，下面的过程描述现在，若要获取的正确版本[FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) bioconductor，假定计算机具有 internet 访问权限的包。

1.  在“包存档”列表中，查找“Windows 二进制文件”版本。

2.  右键单击的链接。ZIP 文件，并选择**目标另存为**。

3.  导航到本地文件夹，zip 的包存储中，然后单击**保存**。

此过程将创建包的本地副本。 然后可以安装包，也可将压缩的包复制到的服务器，不能访问 internet。

有关的 zip 文件格式，以及如何创建 R 包内容的详细信息，我们建议本教程中，你可以从 R 项目站点的 PDF 格式下载该：[创建 R 包](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)。

### <a name="bkmk_packageDependencies"></a>获取包的依赖项

R 包经常依赖于多个其他包，其中一些可能不可用的实例所使用的默认 R 库中。 或者，有时包需要已安装的从属包的不同版本。

如果你需要安装多个包，或想要确保你的组织中的每个人都获得正确的包类型和版本，我们建议使用 miniCRAN 包来创建可以在多个用户或计算机之间共享的本地存储库。 有关详细信息，请参阅[创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

### <a name="permissions"></a>Permissions

如果你是经验丰富的 R 用户，你可能会习惯于从命令行无需特殊权限，或不带提前进行下载安装包。 但是，大多数服务器没有 internet 连接。 此外，访问文件共享或存储可能受到限制。

本部分介绍的不同级别的权限所需的安装 SQL Server 2016 和 SQl Server 自 2017 年中的包。 可以安装使用 R 工具或 SQL Server，但略有不同的进程和权限。

-   SQL Server 2016

    在此版本中，仅计算机上的管理员可以安装包，到所需的位置。 使用标准 R 工具来安装包，但你必须以管理员身份运行，并使用与实例关联的 R 工具。

-   SQL Server 2017

    此版本提供了新功能，让数据库管理员委派给用户的包安装。 数据库管理员必须启用基于每个实例的程序包管理功能。 启用此功能后，DBA 可以使用数据库角色授予单个用户安装包，根据需要也可以共享基于每个数据库的包的权限。

    有关详细信息，请参阅[for SQL Server 的 R 包管理](r-package-management-for-sql-server-r-services.md)。


> [!IMPORTANT]
> 
> 有经验的 R 用户习惯于在用户库中，安装包和作为一部分 R 解决方案，然后引用该文件夹中的包，通过指定的文件路径。 但是，在 SQL Server 中不支持这种做法。 有关详细信息和解决方法，请参阅[如何使用用户库中的包](packages-installed-in-user-libraries.md)。

### <a name="comparing-package-management-methods"></a>比较包管理方法

本部分比较包安装方法可用，并列出了一些其他注意事项和提示可帮助你确定适当的包管理和安装策略。

#### <a name="using-sql-server-package-management-features"></a>使用 SQL Server 程序包管理功能

如果启用包管理，则会安装特定数据库的包。 如果你需要使用的包中的所有数据库中启用 R 脚本，必须将安装到每个数据库。

但是，由于 SQL Server 管理有关哪些用户有权使用的包的信息，因此很方便地复制用户和数据库之间的包有关的信息。 也很容易重新生成一组工作包的用户或多个用户数据库，还原时或在实例之间移动时。

在 SQL Server 2017 使用 T-SQL 和程序包管理功能是首选的方法，只要您有多个数据库用户安装或正在运行的 R 包。

此功能是使用 SQL Server 自 2017 年开始提供。

#### <a name="using-r-tools-to-install-packages-for-the-sql-server-instance"></a>使用 R 工具安装的 SQL Server 实例的包

如果使用此方法，将提供任何数据库中的实例安装的程序包。 但是，由于直接发送到文件系统安装包，它们必须在 SQL Server 外部管理。 包不能备份或还原。 此外，数据库管理员必须了解如何使用 R 工具。

但是，此解决方案是最简单的一个，如果你是唯一的数据库所有者。

#### <a name="managing-multiple-packages-and-multiple-versions-of-the-same-package"></a>管理多个包和同一个包的多个版本

如果你需要执行的 R 包的脱机安装，本地存储库使用设置[miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/)可以共享包和由组织管理可供使用的版本。

#### <a name="establish-a-single-mirror-site-as-standard"></a>作为标准建立一个镜像站点

为了避免每次添加新包都必须选择镜像站点，可将 R 开发环境配置为始终使用相同的存储库。 若要执行此操作，编辑全局 R 设置文件， **。Rprofile**，并添加以下行：

`options(repos=structure(c(CRAN="<mirror site URL>")))`

上列出需当前 CRAN 镜像[此站点](https://cran.r-project.org/mirrors.html)。

有关首选项以及 R 运行时启动时加载的其他文件的详细信息，请从 R 控制台运行此命令：`?Startup`

#### <a name="know-which-library-you-are-using-for-installation"></a>了解用于安装的库

如果以前已修改的 R 环境的计算机上，然后才能安装任何内容，暂停一段时间，并确保 R 环境变量`.libPath`使用一个路径。

此路径应指向实例 R_SERVICES 文件夹。 有关详细信息，请参阅[与 SQL Server 安装的 R 包](installing-and-managing-r-packages.md)。

#### <a name="side-by-side-installation-with-r-server"></a>使用 R Server 通过并行安装

如果已安装除了 SQL Server 计算机学习 Services 的 Microsoft 机器学习 Server （独立版），则计算机应该具有单独的安装中的 R 对于每个两者来说，与所有的 R 工具和库的重复项。

> [!IMPORTANT]
> 
> 安装到 R_SERVER 库的包只由 Microsoft R Server 和 SQL Server 无法访问。
> 
> 请务必使用`R_SERVICES`库安装你想要使用 SQL Server 中的包时。
