---
title: "创建本地包存储库使用 miniCRAN |Microsoft 文档"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: "4"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 066e09747684ede5837d93736f32792736b8985d
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="create-a-local-package-repository-using-minicran"></a>创建本地包存储库使用 miniCRAN

有两种方法可以用于为进行 internet 访问服务器上的安装准备 R 包。

-   [使用 miniCRAN 包创建一个本地存储库](#bkmk_miniCRAN)

    [MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)创建包含类似 CRAN 的存储库中的所选包的内部一致存储库。 用户指定一组所需的包和 miniCRAN 以递归方式读取这些包的依赖关系树，并下载仅列出的包和其依赖项。

    然后可以将此本地存储库移到服务器，并继续安装而不使用 internet 的包。

-   [手动下载并将包逐个复制](#bkmk_manual)

    你可以下载的包的描述文件中找到从属包的列表。 
    
    但是，包列入**导入**可能存在第二级依赖关系。 为此，我们建议使用**miniCRAN**方法。

> [!TIP]
> 你知道你可以使用 miniCRAN 准备包在 Azure 机器学习中使用吗？ 有关详细信息，请参见以下博客： [Azure ML，通过王小兰 Usuelli 中使用 miniCRAN](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="prepare-packages-using-minicran"></a>准备使用 miniCRAN 包

创建本地包存储库的目的是提供服务器管理员或其他组织中的用户可以使用在无 internet 访问权限的服务器上安装新的 R 包的单个位置。

[MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)打包为 R 编写的[Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)以更加轻松地创建一致的托管的组织的 R 程序包集。 

有很多好处使用 miniCRAN 来创建存储库：

-   **安全**： 许多 R 用户习惯于下载和安装新的 R 包，随意情况下，从 CRAN 或其镜像站点之一。 但是，出于安全原因，生产服务器运行[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]通常没有 internet 连接。

-   **更轻松地脱机安装**： 若要将程序包安装到脱机的服务器，需要，你还可以下载所有包依赖项，使用 miniCRAN，更便于在正确的格式中获取所有依赖项。

-   **改进的版本管理**： 在多用户环境中，有很好的理由，为了避免不受限制的安装在服务器上的多个包版本。

创建之后存储库，你可以修改它通过添加新包或现有包的版本升级。

> [!NOTE]
> MiniCRAN 包本身是依赖于 18 其他 CRAN 包，在其中是 RCurl 包，后者在 curl devel 包上具有系统依赖项。 同样，包 XML libxml2 devel 具有的依赖关系。 因此，我们建议你生成本地存储库最初具有完全的 Internet 访问权限的计算机上，以便你可以轻松地满足所有这些依赖关系。 创建后，你可以移动到其他位置存储库。

### <a name="step-1-install-the-minicran-package"></a>步骤 1. 安装 miniCRAN 包

你首先创建一个 miniCRAN 存储库，以用作源。 你应在具有 internet 访问权限的计算机上创建此存储库。

1.  安装 miniCRAN 包和所需**igraph**包。

    ```R
    if(!require("miniCRAN")) install.packages("miniCRAN") if(!require("igraph"))
    install.packages("igraph") library(miniCRAN)
    ```

### <a name="step-2-define-a-package-source-a-cran-mirror-or-an-mran-snapshot"></a>步骤 2. 定义包源： CRAN 镜像或 MRAN 快照

1. 指定要在获取包中使用的镜像站点。

    ```R
    CRAN_mirror \<- c(CRAN = "https://mran.microsoft.com/snapshot/2017-08-01")
    ```

2.  键入要在其中存储收集的包的本地文件夹的名称。 

    请确保事先创建文件夹。 如果引发错误`local_repo`文件夹不存在时更高版本运行的 R 代码。

    文件夹应具有的描述性名称。 例如，请避免使用"miniCRAN"，并改为类似"GeneticsPackages"或"TeamRPackages1.0.2"中键入的内容。

    ```R
    local_repo <- "~/miniCRAN"
    ```

    波形符扩展运算符返回的环境变量，结果等效于`Sys.getenv("R_USER")`。

### <a name="step-3-add-packages-to-the-repository"></a>步骤 3. 将程序包添加到存储库

1.  安装 miniCRAN 后，创建指定你想要下载的其他包的列表。

    向此初始列表; 不会添加任何依赖项**igraph** miniCRAN 所使用的包将为你生成依赖项列表。 有关如何使用生成的依赖项关系图的详细信息，请参阅[使用 miniCRAN 来标识包的依赖项](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)。

    下面的 R 脚本演示如何获取目标包、"zoo"和"预测"。

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```
2. 它不需要你绘制依赖项关系图中，但它会提供有用的信息。
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 创建本地存储库。 请务必更改的 R 版本，如有必要

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror)
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3")
    ```

    中的信息，则 miniCRAN 程序包会创建您需要将复制到包的文件夹结构[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]更高版本。

4. 此时应具有包含需要包的文件夹并需要的任何其他包的。

    你可以运行下面的代码，若要列出 miniCRAN 存储库中所含的包。

    ```R
    pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE)
    head(pdb)
    pdb$Package
    pdb[, c("Package", "Version", "License")]
    ```

### <a name="step-4-use-the-repository-to-add-r-packages-to-the-instance-library"></a>步骤 4. 使用存储库来将 R 包添加到实例库

你已经创建了存储库并将添加所需的包后，必须将程序包存储库移到服务器计算机上，并确保 R 包一起安装在用于从 SQL Server 使用的正确库。

具体取决于 SQL Server 的版本，有两个选项用于向与 SQL Server 实例关联的 R 库中添加新的包：

- 将安装到使用 miniCRAN 存储库和 R 工具的实例库。

- 将包上载到 SQL Server 数据库，并使用创建外部库语句进行安装。 此选项需要 SQL Server 自 2017 年。 请参阅[在 SQL Server 上安装其他 R 包](install-additional-r-packages-on-sql-server.md)。

以下过程描述如何使用安装包 R 工具。

1. 将复制包含 miniCRAN 存储库，其完整，到你计划安装这些包的服务器的文件夹。

2. 打开 R 命令提示符使用与实例关联的 R 工具。

    - 对于 SQL Server 自 2017 年，默认文件夹是`C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`。

    - 对于 SQL Server 2016，默认文件夹是 `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`。

    - 对于命名实例，该默认路径将为类似于： `<instance_path>.RTEST/R_SERVICES/library`。

    -  如果你将 SQL Server 安装到了一个不同的驱动器，或者在安装路径中执行了任何其他更改，请务必同样执行这些更改。

3.  获取实例库的路径，并将其添加到的库路径的列表。

    ```R
    .libPaths()[1]  
    lib \<- .libPaths()[1]
    ```

    在 SQL Server 上，此命令应返回与该实例，如关联的库的路径:"c: / Program 文件/Microsoft SQL Server/MSSQL14。MSSQLSERVER/R_SERVICES/库"

4.  指定在其中复制 mininCRAN 存储库中的服务器上的位置`server_repo`。

    在此示例中，我们假设存储库复制到你在服务器上的用户文件夹。

    ```R
    R server_repo <- "C:\\Users\\MyUserName\\miniCRAN"
    ```

5.  由于在服务器上新的 R 工作区中操作，你还必须提供要安装程序包的列表。

    ```R
    tspackages <- c("zoo", "forecast")
    ```

6.  提供 miniCRAN 存储库的本地副本路径的包安装。

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath(server_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE)
    ```

7.  从实例库中，你可以查看已安装的软件包使用类似于以下命令：

    ```R
    installed.packages()
    ```

> [!NOTE] 
> 在 SQL Server，服务器管理员必须包从 miniCRAN 存储库安装到的实例使用的默认库。 

## <a name="manually-download-single-packages"></a>手动下载单个包

如果你不希望使用 miniCRAN，你可以手动下载你需要的包以及其依赖项。 若要执行此操作需要您是管理员或服务器的唯一所有者。

在下载包之后, 从压缩的文件位置安装 R 包。

1. 下载包 zip 文件，并将它们保存在本地文件夹

2. 将复制到该文件夹[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]计算机。

3. 将包安装到 SQL Server 实例库。

> [!NOTE]
> 当你使用 R 工具安装包时，它们将安装的实例作为一个整体。 
> 
> 如果你想要将程序包安装到数据库以及与使用数据库角色的用户共享包，则必须上载使用创建外部库语句的库。 请参阅[在 SQL Server 中安装其他 R 包](install-additional-r-packages-on-sql-server.md)
