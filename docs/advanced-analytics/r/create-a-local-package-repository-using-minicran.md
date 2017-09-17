---
title: "使用 miniCRAN 创建本地包存储库 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8af93b3e132290eef4b43da568b9381ff8e5a04
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-local-package-repository-using-minicran"></a>使用 miniCRAN 创建本地包存储库
本主题介绍了如何使用 R 包 **miniCRAN** 创建本地 R 包存储库。 

因为 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例通常位于没有 Internet 连接的服务器上，所以，用于安装 R 包的标准方法（R 命令 `install.packages()`）可能无法工作，因为包安装程序无法访问 CRAN 或任何其他镜像站点。

从本地共享或存储库安装包时有两个选项可供选择：

+ 使用 miniCRAN 包为你需要的包创建一个本地存储库，然后从此存储库进行安装。 本主题介绍了 miniCRAN 方法。

+ 将你需要的包及其依赖项下载为 zip 文件，将它们保存到一个本地文件夹中，然后将该文件夹复制到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机。 有关手动复制方法的详细信息，请参阅[在 SQL Server 上安装其他包](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)。


## <a name="step-1-install-minicran-and-download-packages"></a>步骤 1. 安装 miniCRAN 并下载包 


1. 在能够访问 Internet 的计算机上安装 miniCRAN 包。

   ~~~~
   # Install miniCRAN and igraph

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. 使用以下 R 脚本将你需要的包下载或安装到此计算机。 这将创建你以后将包复制到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 时所需的文件夹结构。

   ~~~~
   # List the packages to get. Do not specify dependencies.
   pkgs_needed <- c("ggplot2", "ggdendro")
   # Plot the dependency graph 
   plot(makeDepGraph(pkgs_needed)) 
   
   # Create the local repo 
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror) 
   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.2") 

   # List local packages 
   pdb <- as.data.frame( 
     pkgAvail(local_repo, type = "win.binary", Rversion = "3.2"),  
     stringsAsFactors = FALSE) 
   head(pdb) 
   pdb$Package 
   pdb[, c("Package", "Version", "License")] 
   ~~~~


## <a name="step-2-copy-the-minicran-repository-to-the-sql-server-computer"></a>步骤 2. 将 miniCRAN 存储库复制到 SQL Server 计算机 

将 miniCRAN 存储库复制到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例上的 R_SERVICES 库。

+ 对于 SQL Server 2016，默认文件夹是 `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library1`。
+ 对于 SQL Server 自 2017 年，默认文件夹是`C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library1`。

如果你使用已命名实例安装了 R Services，请务必在路径中包括实例名称，以确保将库安装到正确的实例。 例如，如果你的已命名实例为 RTEST02，则该已命名实例的默认路径将是：`C:\Program Files\Microsoft SQL Server\MSSQL13.RTEST02\R_SERVICES\library`。

如果你将 SQL Server 安装到了一个不同的驱动器，或者在安装路径中执行了任何其他更改，请务必同样执行这些更改。

## <a name="step-3-install-the-packages-on-sql-server-using-the-minicran-repository"></a>步骤 3. 使用 miniCRAN 存储库在 SQL Server 上安装包

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机上，以管理员身份打开 R 命令行或 RGUI。 
  
> [!TIP]
> 你在该计算机上可能具有多个 R 库；因此，为确保将包安装到正确的实例，请使用随你要在其中安装包的特定实例安装的 RGUI 或 RTerm 的副本。
  
当提示指定一个存储库时，选择包含你刚才复制的文件的文件夹，即本地 miniCRAN 存储库。

   ~~~~
   # Run this R code as administrator on the SQL Server computer 
   pkgs_needed <- c("ggplot2", "ggdendro") 
   local_repo  <- "~/miniCRAN" 

   # OPTIONAL: If you are not running R from the instance library as recommended, you must specify the path
   #   .libPaths()[1] 
   # "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library " 
   # lib <- .libPaths()[1]
   
   install.packages(pkgs_needed,  
                    repos = file.path("file://", normalizePath(local_repo, winslash = "/")), 
                    lib = lib, 
                    type = "win.binary", 
                    dependencies = TRUE 
                    ) 
   installed.packages() 
   ~~~~

验证包是否已安装。
   ~~~~
   installed.packages()
   ~~~~



## <a name="acknowledgements"></a>致谢

此信息源自 miniCRAN 包的开发者 Andre de Vries 编写的以下文章。 有关详细信息和完整演练，请参阅 [How to install R packages on an off-line SQL Server 2016 instance](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)（如何在脱机 SQL Server 2016 实例上安装 R 包）

