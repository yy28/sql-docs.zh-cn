---
title: "创建本地包存储库使用 miniCRAN |Microsoft 文档"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 1dd7e8f1a0054818849b3b9672a5df6286bdabce
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

---
# <a name="create-a-local-package-repository-using-minicran"></a>创建本地包存储库使用 miniCRAN

有两种方法可以用于为进行 internet 访问服务器上的安装准备 R 包。

-   [使用 miniCRAN 包创建一个本地存储库](#bkmk_miniCRAN)

    [MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)创建包含类似 CRAN 的存储库中的所选包的内部一致存储库。 用户指定一组所需的包和 miniCRAN 以递归方式读取这些包的依赖关系树，并下载仅列出的包和其依赖项。

    然后可以将此本地存储库移到服务器，并继续安装而不使用 internet 的包。

-   [手动下载并将包逐个复制](#bkmk_manual)

本指南介绍了如何创建 R 程序包存储库使用这两种方法，并建议使用的**miniCRAN**包。

## <a name="prepare-packages-using-minicran"></a>准备使用 miniCRAN 包

创建本地包存储库的目的是提供服务器管理员或其他组织中的用户可以使用在无 internet 访问权限的服务器上安装新的 R 包的单个位置。

[MiniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)打包为 R 编写的[Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)以更加轻松地创建一致的托管的组织的 R 程序包集。 

有很多好处使用 miniCRAN 来创建存储库：

-   **安全**： 许多 R 用户习惯于下载和安装新的 R 包，随意情况下，从 CRAN 或其镜像站点之一。 但是，出于安全原因，生产服务器运行[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]通常没有 internet 连接。

-   **更轻松地脱机安装**： 若要将程序包安装到脱机的服务器，需要，你还可以下载所有包依赖项，使用 miniCRAN，更便于在正确的格式中获取所有依赖项。

-   **改进的版本管理**： 在多用户环境中，有很好的理由，为了避免不受限制的安装在服务器上的多个包版本。

创建之后存储库，你可以修改它通过添加新包或现有包的版本升级。

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

2.  指示要在其中存储收集的包的本地文件夹。 您不需要命名文件夹 miniCRAN 中;它可能是更具描述性的名称，例如"GeneticsPackages"或"ClientRPackages1.0.2"。

    只需请确保事先创建文件夹。 如果引发错误`local_repo`文件夹不存在时更高版本运行的 R 代码。

    ```R
    local_repo <- "~/miniCRAN"
    ```

    波形符扩展运算符返回的环境变量，结果等效于`Sys.getenv("R_USER")`。

### <a name="step-3-add-packages-to-the-repository"></a>步骤 3. 将程序包添加到存储库

1.  安装 miniCRAN 后，创建指定你想要下载的其他包的列表。

    向此初始列表; 不会添加任何依赖项**igraph** miniCRAN 所使用的包将为你生成依赖项列表。 有关如何使用此图的详细信息，请参阅[使用 miniCRAN 来标识包的依赖项](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)。

    下面的 R 脚本演示如何获取目标包、"zoo"和"预测"。

    ```R
    pkgs_needed <- c("zoo", "forecast")

2. Optionally, plot the dependency graph, which can be informative and looks cool.
    
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

-   将安装到使用 miniCRAN 存储库和 R 工具的实例库。

-   将包上载到 SQL 数据库，并借助创建外部库语句为每个数据库分别安装程序包。 请参阅[在 SQL Server 上安装其他 R 包](install-additional-r-packages-on-sql-server.md)。

以下过程描述如何使用安装包 R 工具。

1.  将复制包含 miniCRAN 存储库，其完整，将在其中安装包的服务器到的文件夹。

2.  打开 R 命令提示符使用与实例关联的 R 工具。

    - 对于 SQL Server 自 2017 年，默认文件夹是`C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`。

    - 对于 SQL Server 2016，默认文件夹是 `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`。

    - 对于命名实例，该默认路径将为类似于： `<instance_path>.RTEST/R_SERVICES/library`。

    -  如果你将 SQL Server 安装到了一个不同的驱动器，或者在安装路径中执行了任何其他更改，请务必同样执行这些更改。

3.  （在情况下你的用户目录中），实例库中获取的路径，并将其添加到的库路径的列表。

    ```R
    .libPaths()[1]  
    lib \<- .libPaths()[1]
    ```

    这应会返回实例路径，"c: / Program 文件/Microsoft SQL Server/MSSQL14。MSSQLSERVER/R_SERVICES/库"

2.  指定在其中复制 mininCRAN 存储库中的服务器上的位置`server_repo`。

    在此示例中，我们假设存储库复制到你在服务器上的用户文件夹。

    ```R
    R server_repo <- "C:\\Users\\MyUserName\\miniCRAN"
    ```

3.  由于在服务器上新的 R 工作区中操作，你还必须提供要安装程序包的列表。

    ```R
    tspackages <- c("zoo", "forecast")
    ```

4.  使用安装包，miniCRAN 存储库的本地副本的路径。

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath(server_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE)
    ```

5.  现在，查看已安装的软件包。

    ```R
    installed.packages()
    ```

> [!NOTE] 
> 
> 在 SQL Server 自 2017 年，其他数据库角色和 T-SQL 语句来提供可帮助服务器管理员通过包管理权限。 如果需要的话，请使用 R 或 T-SQL 的数据库管理员可以拥有安装包时，的任务。 但是，DBA 还可以使用角色来使用户能够安装其自己的包。 有关详细信息，请参阅[for SQL Server 的 R 包管理](r-package-management-for-sql-server-r-services.md)。
> 
> 在 SQL Server 2016 中，服务器管理员必须包从 miniCRAN 存储库安装到的实例使用的默认库。 若要执行此操作，使用的 R 工具中所述[前面部分](#bkmk_Rtools)。

## <a name="manually-download-single-packages"></a>手动下载单个包

如果你不希望使用 miniCRAN，你可以手动下载你需要的包以及其依赖项。 若要执行此操作需要您是管理员或服务器的唯一所有者。

在下载包之后, 从压缩的文件位置安装 R 包。

1.  下载包 zip 文件，并将它们保存在本地文件夹

2.  将复制到该文件夹[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]计算机。

3.  将包安装到 SQL Server 实例库。

> [!NOTE]
> 当你使用 R 工具安装包时，它们将安装的实例作为一个整体。 
> 
> 如果你想要将程序包安装到数据库以及与使用数据库角色的用户共享包，则必须上载使用创建外部库语句的库。 请参阅[在 SQL Server 中安装其他 R 包](install-additional-r-packages-on-sql-server.md)

