---
title: 创建本地 R 包存储库使用 miniCRAN-SQL Server 机器学习服务
description: 使用 miniCran 检测、 汇编和到一个统一包中安装 R 包依赖项。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: d9154bc1c01bdf9bd7bdfd7a4032b4ed173464d6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642602"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>创建本地 R 包存储库使用 miniCRAN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)创建的包[Andre de Vries](https://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)、 标识和下载包和依赖项的单个文件夹，您可以将其复制到脱机的 R 包安装其他计算机。

作为输入，指定一个或多个包。 **miniCRAN**以递归方式读取这些包的依赖关系树，并从 CRAN 或类似的存储库下载仅列出的包及其依赖项。

作为输出， **miniCRAN**创建包含所选的包和所需的所有依赖项的内部一致存储库。 然后可以将此本地存储库移到服务器，并继续在安装包未连接到 internet。

> [!NOTE]
> 有经验的 R 用户通常查找下载的包的 DESCRIPTION 文件中的相关程序包的列表。 但是，包列入**导入**可能具有第二个级别的依赖项。 出于此原因，我们建议**miniCRAN**的组合所需的包的完整集合。

## <a name="why-create-a-local-repository"></a>为什么要创建本地存储库

创建本地包存储库的目的是提供服务器管理员或组织中的其他用户可以使用新的 R 包安装在服务器上，尤其是一个不具有 internet 访问的单个位置。 在创建之后存储库，您可以修改它通过添加新的包或升级现有包的版本。

包存储库可在这些情况下：

- **安全**:许多 R 用户习惯于下载和安装在将新的 R 包从 CRAN 或某个及其镜像站点。 但是，出于安全原因，生产服务器运行[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]通常未建立 internet 连接。

- **更轻松地脱机安装**:若要将程序包安装到脱机的服务器需要，您还可以下载所有包依赖项，通过使用 miniCRAN 可以更轻松地获取正确格式的所有依赖项。

    通过使用 miniCRAN，您可以避免包依赖项错误，准备要使用安装包时[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)语句。

- **改进的版本管理**:在多用户环境中，有充分的理由，为了避免不受限制的安装在服务器上的多个包版本。 使用本地存储库以供分析师提供一组一致的包。 

> [!TIP]
> MiniCRAN 还可用于准备在 Azure 机器学习中使用的包。 有关详细信息，请参阅此博客：[在 Azure ML 中，通过 Michele Usuelli 使用 miniCRAN](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>安装 miniCRAN

**MiniCRAN**包本身是依赖于其他 18 CRAN 包，即之间**RCurl**包，其中包含系统依赖项上**curl 开发**包。 同样，打包**XML**依赖**libxml2 开发**。 若要解决依赖项，我们建议你生成在本地存储库最初具有完全访问 internet 的计算机上。 

使用基础 R，在计算机上运行以下命令的 R 工具和 internet 连接。 假定这是*不*SQL Server 计算机。 下面的命令安装**miniCRAN**包和所需**igraph**包。 此示例检查是否已安装此包，但您可以跳过 if 语句，并直接安装包。

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>设置的 CRAN 镜像和 MRAN 快照

指定要在获取包中使用的镜像站点。 例如，可以在包含所需的包的区域中使用 MRAN 站点或任何其他站点。 如果下载失败，请尝试另一个镜像站点。

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>创建一个本地文件夹

创建本地文件夹，例如`C:\mylocalrepo`要在其中存储收集的包。 如果经常重复此，您可能应使用更具说明性的名称，例如"miniCRANZooPackages"或"miniCRANMyRPackagev2"。

为本地存储库中指定的文件夹。 R 语法使用正斜杠的路径名称，这是另一 Windows 约定。

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>将包添加到本地存储库

之后**miniCRAN**安装并加载，创建一个列表，其中指定你想要下载的其他包。

不要**不**将依赖项添加到此初始列表。 **Igraph**使用包**miniCRAN**为您生成依赖项的列表。 有关如何使用生成依赖项关系图的详细信息，请参阅[使用 miniCRAN 标识包的依赖项](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)。

1. 添加目标包、"匹配 zoo"和"forecast"给一个变量。

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. （可选） 绘制依赖项关系图中，但它可以是信息性。
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 创建本地存储库。 请务必更改 R 版本，如有必要为 SQL Server 实例上安装的版本。 版本 3.2.2 是 SQL Server 2016 上，版本 3.3 是在 SQL Server 2017。 如果执行组件升级，你的版本可能更高版本。 有关详细信息，请参阅[获取 R 和 Python 包信息](determine-which-packages-are-installed-on-sql-server.md)。

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   MiniCRAN 包中的信息，创建您需要将包复制到的文件夹结构[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]更高版本。

此时应具有一个包含你需要的包的文件夹和所需的任何其他包了。 路径应类似于以下示例：C:\mylocalrepo\bin\windows\contrib\3.3 和它应包含压缩包的集合。 不要将解压缩包或重命名的任何文件。

（可选） 运行以下代码，以列出本地 miniCRAN 存储库中包含的包。

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>将包添加到实例库

具有所需的包的本地存储库后，将包存储库移到 SQL Server 计算机。 以下过程介绍如何安装使用的 R 工具的包。

1. 将复制包含 miniCRAN 存储库，其无法全部展示，到您计划安装包的服务器中的文件夹。 该文件夹通常具有以下结构： miniCRAN 根 > bin > windows > contrib > 版本 > 的所有包。 在以下示例中，我们假设关闭根驱动器的文件夹： 

2. 打开与实例关联的 R 工具 （例如，可以使用 Rgui.exe）。 右键单击**以管理员身份运行**以允许对系统进行更新的工具。

    - 对于 SQL Server 2017，RGUI 的文件位置是`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`。

    - 对于 SQL Server 2016 中，他 RGUI 文件位置是`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 获取实例库的路径，并将其添加到的库路径的列表。 在 SQL Server 2017 的路径是类似于下面的示例。

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. 指定你复制的服务器上的新位置**miniCRAN**存储库中，作为`server_repo`。

    在此示例中，我们假定您将在存储库复制到服务器上的临时文件夹。

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. 由于要使用在服务器上新的 R 工作区中，您还必须提供要安装包的列表。

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. 安装包，提供 miniCRAN 存储库的本地副本的路径。

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. 从实例库，可以查看已安装的包使用的命令如下所示：

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>另请参阅

+ [获取包信息](determine-which-packages-are-installed-on-sql-server.md)
+ [R 教程](../tutorials/sql-server-r-tutorials.md)
+ [操作指南](sql-server-machine-learning-tasks.md)


