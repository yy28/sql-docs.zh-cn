---
title: 使用 miniCRAN 创建本地 R 包存储库
description: 使用 miniCran 检测、组装 R 包依赖项并将其安装到单个合并的包中。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: e6d204b7f0e2ab0207b22a5e61e1e266a813f195
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345161"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>使用 miniCRAN 创建本地 R 包存储库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) package, 由[Andre de Vries](https://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)创建, 标识并将包和依赖项下载到一个文件夹中, 你可以将其复制到其他计算机以进行脱机 R 包安装。

输入指定一个或多个包。 **miniCRAN**以递归方式读取这些包的依赖关系树, 并仅下载列出的包及其依赖项 (来自 CRAN 或类似的存储库)。

作为输出, **miniCRAN**会创建内部一致的存储库, 其中包含所选包和所有必需的依赖项。 然后, 你可以将此本地存储库移动到服务器上, 并在没有 internet 连接的情况下继续安装包。

> [!NOTE]
> 经验丰富的 R 用户经常会在下载包的描述文件中查找依赖包的列表。 但是,**导入**中列出的包可能有二级依赖项。 出于此原因, 我们建议将**miniCRAN**用于组装所需包的完整集合。

## <a name="why-create-a-local-repository"></a>为什么创建本地存储库

创建本地包存储库的目的是提供一个单一位置, 组织中的服务器管理员或其他用户可以使用该位置在服务器上安装新的 R 包, 特别是没有 internet 访问权限的用户。 在创建存储库后, 可以通过添加新包或升级现有包的版本来修改它。

包存储库在以下情况下很有用:

- **安全性**:许多 R 用户习惯于从 CRAN 或它的某个镜像站点下载和安装新的 R 包。 然而, 出于安全原因, 运行[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]的生产服务器通常没有 internet 连接。

- **脱机安装更简单**:若要将包安装到脱机服务器, 还需要下载所有包依赖项, 使用 miniCRAN 可以更轻松地获取正确格式的所有依赖项。

    通过使用 miniCRAN, 你可以在使用[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)语句准备要安装的包时避免出现包依赖关系错误。

- **改进了版本管理**:在多用户环境中, 有充分的理由来避免在服务器上安装多个包版本。 使用本地存储库提供一组一致的包供分析师使用。 

> [!TIP]
> 你还可以使用 miniCRAN 来准备要在 Azure 机器学习中使用的包。 有关详细信息, 请参阅此博客:[通过 Michele Usuelli 在 Azure ML 中使用 miniCRAN](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>安装 miniCRAN

**MiniCRAN**包本身依赖于18个其他 CRAN 包, 其中是**RCurl**包, 它与**卷 unixodbc-devel**包之间存在依赖关系。 同样, 包**XML**依赖于**libxml2-unixodbc-devel**。 若要解决依赖关系, 建议最初在具有完全 internet 访问权限的计算机上构建本地存储库。 

在具有基本 R、R 工具和 internet 连接的计算机上运行以下命令。 假定这*不*是您 SQL Server 的计算机。 以下命令安装**miniCRAN**包和所需的**igraph**包。 此示例将检查是否已安装包, 但可以绕过 if 语句并直接安装包。

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>设置 CRAN 镜像和 MRAN 快照

指定用于获取包的镜像站点。 例如, 你可以使用 MRAN 站点或区域中包含所需包的任何其他站点。 如果下载失败, 请尝试另一个镜像站点。

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>创建本地文件夹

创建本地文件夹, 例如`C:\mylocalrepo`要在其中存储所收集包的。 如果经常重复此操作, 则可能会使用更具描述性的名称, 如 "miniCRANZooPackages" 或 "miniCRANMyRPackagev2"。

将文件夹指定为本地存储库。 R 语法为路径名称使用正斜杠, 这与 Windows 约定相反。

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>将包添加到本地存储库

安装并加载**miniCRAN**后, 请创建一个列表, 指定要下载的其他包。

不要向此初始**列表添加依赖**项。 **MiniCRAN**使用的**igraph**包为你生成依赖项列表。 有关如何使用生成的依赖项关系图的详细信息, 请参阅[使用 miniCRAN 识别包依赖关系](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)。

1. 将目标包 "zoo" 和 "预测" 添加到变量。

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. (可选) 绘制依赖项关系图, 但它可以是信息性的。
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 创建本地存储库。 如果需要, 请务必将 R 版本更改为 SQL Server 实例上安装的版本。 版本 3.2.2 SQL Server 2016, 版本 3.3 SQL Server 2017。 如果你执行了组件升级, 则你的版本可能会比较新。 有关详细信息, 请参阅[获取 R 和 Python 包信息](../package-management/installed-package-information.md)。

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   通过此信息, miniCRAN 包将创建要将包复制到[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]后面的文件夹结构。

此时, 应该有一个文件夹包含所需的包以及所需的任何其他包。 路径应类似于以下示例:C:\mylocalrepo\bin\windows\contrib\3.3, 它应包含压缩包的集合。 请勿解压缩包或重命名任何文件。

或者, 运行以下代码以列出本地 miniCRAN 存储库中包含的包。

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>将包添加到实例库

使用所需包的本地存储库后, 将包存储库移到 SQL Server 计算机。 以下过程描述如何使用 R 工具安装包。

1. 将包含 miniCRAN 存储库的文件夹整体复制到计划安装包的服务器。 文件夹通常具有以下结构: miniCRAN 根 > bin > windows > contrib > 版本 > 所有包。 在下面的示例中, 我们假设根驱动器上有一个文件夹: 

2. 打开与实例关联的 R 工具 (例如, 可以使用 Rgui.exe)。 右键单击 "以**管理员身份运行**", 以允许该工具对系统进行更新。

    - 对于 SQL Server 2017, RGUI.EXE 的文件位置是`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`。

    - 对于 SQL Server 2016, RGUI.EXE 的文件位置是`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 获取实例库的路径, 并将其添加到库路径列表。 在 SQL Server 2017 上, 路径类似于以下示例。

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. 在复制**miniCRAN**存储库的服务器上指定新位置, 如`server_repo`。

    在此示例中, 我们假定已将存储库复制到服务器上的临时文件夹。

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. 由于你在服务器上的新 R 工作区中工作, 你还必须为要安装的程序包列出。

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. 安装包, 提供 miniCRAN 存储库的本地副本的路径。

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. 从实例库中, 可以使用如下所示的命令查看已安装的包:

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>请参阅

+ [获取包信息](../package-management/installed-package-information.md)
+ [R 教程](../tutorials/sql-server-r-tutorials.md)
