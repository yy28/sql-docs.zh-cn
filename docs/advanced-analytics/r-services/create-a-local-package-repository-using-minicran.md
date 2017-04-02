---
title: "创建本地包存储库使用 miniCRAN | Microsoft Docs"
ms.custom: ""
ms.date: "05/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 4
---
# 创建本地包存储库使用 miniCRAN
本主题介绍如何创建本地 R 程序包存储库使用 R 包 **miniCRAN**。 

因为 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例通常位于服务器上没有 Internet 连接，安装多个 R 包的标准方法 (R 命令 `install.packages()`) 可能不起作用，因为程序包安装程序无法访问 CRAN 或任何其他镜像站点。

有两个选项可用于从本地共享或存储库安装包︰

+ 使用 miniCRAN 包创建的包需要则此存储库中安装的本地存储库。 本主题介绍 miniCRAN 方法。

+ 下载您需要的包以及其依赖项，为 zip 文件，然后将它们保存在本地文件夹，然后将复制到该文件夹 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机。 手动复制方法的详细信息，请参阅 [在 SQL Server 上安装其他程序包](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)。


## 步骤 1. 安装 miniCRAN 并下载包 


1. 在具有 Internet 访问权限的计算机上安装 miniCRAN 包。

   ~~~~
   # Install miniCRAN ---------------------------------------------------

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. 下载或安装到此计算机所需的包。 这将创建您需要将复制到包的文件夹结构 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 更高版本。

   ~~~~
   # List the packages you need 
   # Do not specify dependencies
   pkgs_needed <- c("ggplot2", "ggdendro")
   ~~~~

3. 将 miniCRAN 存储库复制到 R_SERVICES 库上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例。

## 步骤 2. SQL Server 计算机上安装包 

4. 在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 运行 R 命令的计算机  `install.packages()`。 您可以使用与安装的 R 工具之一 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], ，如 Rgui.exe，或者您可以运行命令的一部分 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 存储过程。
5. 在提示符下，若要指定一个存储库中，选择包含这些文件的文件夹，您只需复制;也就是说，本地 miniCRAN 存储库。

   ~~~~
   pkgs_needed <- c("ggplot2", "ggdendro")
   local_repo  <- "~/miniCRAN"
   
   .libPaths()[1]
   "C:/Program Files/Microsoft SQL Server/130/R_SERVER/library"

   lib <- .libPaths()[1]

   install.packages(pkgs_needed, 
                 repos = file.path("file://", normalizePath(local_repo, winslash = "/")),
                 lib = lib,
                 type = "win.binary",
                 dependencies = TRUE
                 )
   ~~~~

6. 验证包已安装运行此 R 代码。
   ~~~~
   installed.packages()
   ~~~~



## 确认

此信息的源是由 Andre de Vries，还开发了 miniCRAN 包这篇文章。 有关详细信息和完整的演练，请参阅  [离线的 SQL Server 2016 实例上如何安装 R 包](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)