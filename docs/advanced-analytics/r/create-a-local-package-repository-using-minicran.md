---
title: 创建本地 R 程序包存储库使用 miniCRAN （SQL Server 机器学习） |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4ce6479c0e7087e63271811abb47a2174747638e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>创建使用 miniCRAN 本地 R 程序包存储库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)包由 Andre de Vries 以支持这些常见的方案： 

+ 分析单个包或组的包的包依赖关系
+ 正在为安装到没有 internet 访问权限的服务器上准备一组 R 包。

用户指定一组所需的包和 miniCRAN 以递归方式读取这些包的依赖关系树，并从 CRAN 或类似的存储库下载仅列出的包和其依赖项。

作为输出，miniCRAN 创建所选的包和所有必需的依赖项组成的内部一致存储库。 然后可以将此本地存储库移到服务器，并继续安装而不使用 internet 的包。

通常情况下，有经验的 R 用户所查找的下载的包的描述文件中的从属包的列表。 但是，包列入**导入**可能存在第二级依赖关系。 为此，我们建议使用**miniCRAN**方法。

## <a name="what-is-a-package-repository"></a>什么是程序包存储库

创建本地包存储库的目的是提供服务器管理员或其他组织中的用户可以使用在无 internet 访问权限的服务器上安装新的 R 包的单个位置。 创建之后存储库，你可以修改它通过添加新包或现有包的版本升级。

[MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)打包为 R 编写的[Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)以更加轻松地创建一致的托管的组织的 R 程序包集。 

包存储库是在这些情况下有用：

- **安全**： 许多 R 用户习惯于下载和安装新的 R 包，随意情况下，从 CRAN 或其镜像站点之一。 但是，出于安全原因，生产服务器运行[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]通常没有 internet 连接。

- **更轻松地脱机安装**： 若要将程序包安装到脱机的服务器，需要，你还可以下载所有包依赖项，使用 miniCRAN，更便于在正确的格式中获取所有依赖项。

    通过使用 miniCRAN，你可以避免包依赖关系错误准备包以使用安装时[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)语句。

- **改进的版本管理**： 在多用户环境中，有很好的理由，为了避免不受限制的安装在服务器上的多个包版本。 使用本地存储库以供分析师提供一组一致的包。 

> [!TIP]
> MiniCRAN 还可用于准备在 Azure 机器学习中使用的包。 有关详细信息，请参见以下博客： [Azure ML，通过王小兰 Usuelli 中使用 miniCRAN](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="prepare-packages-using-minicran"></a>准备使用 miniCRAN 包

**MiniCRAN**包本身是依赖于其他 18 CRAN 包，即之间**RCurl**包，其中具有系统依赖项上**curl devel**包。 同样，打包**XML**具有依赖关系**libxml2 devel**。 

出于这些原因，我们建议你生成本地存储库最初具有完全的 Internet 访问权限的计算机上，以便你可以轻松地满足所有这些依赖关系。 

在创建存储库后，你可以移动到其他位置存储库。

### <a name="step-1-install-the-minicran-package"></a>步骤 1. 安装 miniCRAN 包

首先，创建的**miniCRAN**要用作源存储库。 你应在具有 internet 访问权限的计算机上创建此存储库。

1. 安装**miniCRAN**包和所需**igraph**包。 此示例检查是否已安装此包，但你可以绕过 if 语句并直接安装程序包。

    ```R
    if(!require("miniCRAN")) install.packages("miniCRAN") 
    if(!require("igraph")) install.packages("igraph") 
    library("miniCRAN")
    ```

### <a name="step-2-define-a-package-source-a-cran-mirror-or-an-mran-snapshot"></a>步骤 2. 定义包源： CRAN 镜像或 MRAN 快照

1. 指定要在获取包中使用的镜像站点。 例如，你可以在包含你需要的软件包您所在地区使用 MRAN 站点或任何其他站点。 如果下载失败，请尝试另一个镜像站点。

    ```R
    CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
    CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
    ```

2. 键入要在其中存储收集的包的本地文件夹的名称。 

    请确保事先创建文件夹。 如果引发错误`local_repo`文件夹不存在时更高版本运行的 R 代码。

    文件夹应具有的描述性名称。 此处我们使用了"miniCRAN"，但如果重复这通常，你可能应使用更具描述性的名称，例如"miniCRANZooPackages"或"miniCRANMyRPackagev2"。

    ```R
    local_repo <- "~/miniCRAN"
    ```

    波形符扩展运算符返回的环境变量，结果等效于`Sys.getenv("R_USER")`。

### <a name="step-3-add-packages-to-the-repository"></a>步骤 3. 将程序包添加到存储库

1. 后**miniCRAN**是安装，创建指定你想要下载的其他包的列表。

    执行**不**将依赖项添加到此初始列表。 **Igraph**包使用**miniCRAN**将为你生成依赖项列表。 有关如何使用生成的依赖项关系图的详细信息，请参阅[使用 miniCRAN 来标识包的依赖项](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)。

    下面的 R 脚本将添加目标包，"zoo"以及"预测"到变量。

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```
2. 它不需要你绘制依赖项关系图中，但它会提供有用的信息。
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 创建本地存储库。 请务必更改的 R 版本，如有必要

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

    中的信息，则 miniCRAN 程序包会创建您需要将复制到包的文件夹结构[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]更高版本。

4. 此时应具有包含需要包的文件夹并需要的任何其他包的。

    你可以运行下面的代码，若要列出 miniCRAN 存储库中所含的包。

    ```R
    pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
    head(pdb);
    pdb$Package;
    pdb[, c("Package", "Version", "License")]
    ```

### <a name="step-4-use-the-repository-to-add-r-packages-to-the-instance-library"></a>步骤 4. 使用存储库来将 R 包添加到实例库

你已经创建了存储库并将添加所需的包后，必须将程序包存储库移到服务器计算机上，并确保 R 包一起安装在用于从 SQL Server 使用的正确库。

以下过程描述如何使用安装包 R 工具。

1. 将复制包含 miniCRAN 存储库，其完整，到你计划安装这些包的服务器的文件夹。 该文件夹通常具有此结构： miniCRAN 根 >-> bin-> windows-> contrib-> 版本不-> 所有包。

2. 打开 R 命令提示符使用与实例关联的 R 工具。

    - 对于 SQL Server 自 2017 年，默认文件夹是`C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`。

    - 对于 SQL Server 2016，默认文件夹是 `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`。

    - 对于命名实例，该默认路径将为类似于： `<instance_path>.RTEST/R_SERVICES/library`。

    -  如果你将 SQL Server 安装到了一个不同的驱动器，或者在安装路径中执行了任何其他更改，请务必同样执行这些更改。

3. 获取实例库的路径，并将其添加到的库路径的列表。

    ```R
    .libPaths()[1];
    lib <- .libPaths()[1]
    ```

    在 SQL Server 上，此命令应返回与该实例，如关联的库的路径:"c: / Program 文件/Microsoft SQL Server/MSSQL14。MSSQLSERVER/R_SERVICES/库"

4. 指定复制到其中的服务器上的新位置**miniCRAN**存储库，作为`server_repo`。

    在此示例中，我们假设存储库复制到服务器上的临时文件夹。

    ```R
    source_repo <- "C:\\temp\\miniCRAN"
    ```

5. 由于在服务器上新的 R 工作区中操作，你还必须提供要安装程序包的列表。

    ```R
    tspackages <- c("zoo", "forecast")
    ```

6. 提供 miniCRAN 存储库的本地副本路径的包安装。

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath;(source_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE);
    ```

7. 从实例库中，你可以查看已安装的软件包使用类似于以下命令：

    ```R
    installed.packages()
    ```

> [!NOTE] 
> 若要使用 SQL Server 中的包，包必须安装到的实例使用的默认库中。 

## <a name="manually-install-a-single-package-from-a-zipped-file"></a>从压缩文件中手动安装单个包

如果你正在安装没有依赖关系的单个包，或者不能使用**miniCRAN**，你可以手动下载所需的包。 若要执行此操作需要您是管理员或服务器的唯一所有者。

在下载包之后, 从压缩的文件位置安装 R 包。

1. 下载 zip 文件中，为包，并将其保存在本地文件夹

2. 将复制到该文件夹[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]计算机。

3. 将包安装到 SQL Server 实例库使用传统的 R 命令。 如果包具有已未安装的依赖关系，你没有包括它们，则安装可能会失败。 

你还可以将单个包使用上载到的 SQL Server 2017 实例[创建外部库语句](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。 此过程还需要管理访问权限。
