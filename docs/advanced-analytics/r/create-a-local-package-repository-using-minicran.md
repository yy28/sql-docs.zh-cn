---
title: 创建本地 R 程序包存储库使用 miniCRAN （SQL Server 机器学习） |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1f7ba3b4acde90d9e416eb092ac80cb0dfcbba8a
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34585639"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>创建使用 miniCRAN 本地 R 程序包存储库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)创建的包[Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)、 标识和下载包和单个的文件夹，你可以将复制到其他计算机以执行脱机的 R 包安装到的依赖项。

作为输入，指定一个或多个包。 **miniCRAN**以递归方式读取这些包的依赖关系树，并从 CRAN 或类似的存储库下载仅列出的包和其依赖项。

作为输出， **miniCRAN**创建包含所选的包和所有必需的依赖项的内部一致存储库。 然后可以将此本地存储库移到服务器，并继续安装包未连接到 internet。

> [!NOTE]
> 通常情况下，有经验的 R 用户所查找的下载的包的描述文件中的从属包的列表。 但是，包列入**导入**可能存在第二级依赖关系。 为此，我们建议**miniCRAN**组合所需的程序包的完整集合的。

## <a name="why-create-a-local-repository"></a>为什么要创建本地存储库

创建本地包存储库的目的是提供服务器管理员或其他组织中的用户可以使用的服务器，尤其是不能访问 internet 上安装新的 R 包的单个位置。 创建之后存储库，你可以修改它通过添加新包或现有包的版本升级。

包存储库是在这些情况下有用：

- **安全**： 许多 R 用户习惯于下载和安装新的 R 包，随意情况下，从 CRAN 或其镜像站点之一。 但是，出于安全原因，生产服务器运行[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]通常没有 internet 连接。

- **更轻松地脱机安装**： 若要将程序包安装到脱机的服务器，需要，你还可以下载所有包依赖项，使用 miniCRAN，更便于在正确的格式中获取所有依赖项。

    通过使用 miniCRAN，你可以避免包依赖关系错误准备包以使用安装时[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)语句。

- **改进的版本管理**： 在多用户环境中，有很好的理由，为了避免不受限制的安装在服务器上的多个包版本。 使用本地存储库以供分析师提供一组一致的包。 

> [!TIP]
> MiniCRAN 还可用于准备在 Azure 机器学习中使用的包。 有关详细信息，请参见以下博客： [Azure ML，通过王小兰 Usuelli 中使用 miniCRAN](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>安装 miniCRAN

**MiniCRAN**包本身是依赖于其他 18 CRAN 包，即之间**RCurl**包，其中具有系统依赖项上**curl devel**包。 同样，打包**XML**具有依赖关系**libxml2 devel**。 若要解决依赖项，我们建议你构建本地存储库最初具有完全 internet 访问权限的计算机上。 

使用基的 R 的计算机上运行以下命令 R 工具和 internet 连接。 假设这是*不*SQL Server 计算机。 以下命令安装**miniCRAN**包和所需**igraph**包。 此示例检查是否已安装此包，但你可以绕过 if 语句并直接安装程序包。

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>设置 CRAN 镜像和 MRAN 快照

指定要在获取包中使用的镜像站点。 例如，你可以在包含你需要的软件包您所在地区使用 MRAN 站点或任何其他站点。 如果下载失败，请尝试另一个镜像站点。

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>创建一个本地文件夹

创建本地文件夹，如`C:\mylocalrepo`要在其中存储收集的包。 如果重复这通常，你可能应使用更具描述性的名称，例如"miniCRANZooPackages"或"miniCRANMyRPackagev2"。

为本地存储库中指定的文件夹。 R 语法使用正斜杠的路径名称，即相反从 Windows 约定。

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>将包添加到本地存储库

后**miniCRAN**安装和加载，创建指定你想要下载的其他包的列表。

执行**不**将依赖项添加到此初始列表。 **Igraph**包使用**miniCRAN**将为你生成依赖项列表。 有关如何使用生成的依赖项关系图的详细信息，请参阅[使用 miniCRAN 来标识包的依赖项](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)。

1. 添加目标包，"zoo"以及"预测"到变量。

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. （可选） 绘制依赖项关系图中，但它会提供有用的信息。
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 创建本地存储库。 请务必更改 R 版本，如有必要为 SQL Server 实例上安装的版本。 版本 3.2.2 位于 SQL Server 2016 中，版本 3.3 位于 SQL Server 自 2017 年。 如果你这样做组件升级，你的版本可能是较新。 有关详细信息，请参阅[获取 R 和 Python 包信息](determine-which-packages-are-installed-on-sql-server.md)。

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   中的信息，则 miniCRAN 程序包会创建您需要将复制到包的文件夹结构[!INCLUDE[ssNoVersion_md](..\..\includes\ssnoversion-md.md)]更高版本。

此时应具有包含需要包的文件夹并需要的任何其他包的。 路径应类似于以下示例： C:\mylocalrepo\bin\windows\contrib\3.3 和它应包含压缩的包的集合。 不要解压缩包或重命名任何文件。

或者，运行下面的代码，若要列出本地 miniCRAN 存储库中所含的包。

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>将包添加到实例库

具有所需的包的本地存储库后，将程序包存储库移到 SQL Server 计算机。 以下过程描述如何使用安装包 R 工具。

1. 将复制包含 miniCRAN 存储库，其完整，到你计划安装这些包的服务器的文件夹。 该文件夹通常具有此结构： miniCRAN 根 > bin > windows > contrib > 版本 > 所有包。 在以下示例中，我们假设关闭根驱动器的文件夹： 

2. 打开与实例关联的 R 工具 （例如，你可以使用 Rgui.exe）。 右键单击**以管理员身份运行**若要允许对你的系统进行更新工具。

    - 对于 SQL Server 2017 RGUI 的文件位置是`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`。

    - 对于 SQL Server 2016 RGUI 他文件位置是`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 获取实例库的路径，并将其添加到的库路径的列表。 在 SQL Server 2017 路径是类似于下面的示例。

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. 指定复制到其中的服务器上的新位置**miniCRAN**存储库，作为`server_repo`。

    在此示例中，我们假设存储库复制到服务器上的临时文件夹。

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. 由于在服务器上新的 R 工作区中操作，你还必须提供要安装程序包的列表。

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. 提供 miniCRAN 存储库的本地副本路径的包安装。

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. 从实例库中，你可以查看已安装的软件包使用类似于以下命令：

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>另请参阅

+ [获取包信息](determine-which-packages-are-installed-on-sql-server.md)
+ [R 教程](../tutorials/sql-server-r-tutorials.md)
+ [操作指南](sql-server-machine-learning-tasks.md)


