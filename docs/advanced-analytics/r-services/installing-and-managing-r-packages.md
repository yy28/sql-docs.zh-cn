---
title: "安装和管理多个 R 包 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 安装和管理多个 R 包
 在运行任何 R 解决方案 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 必须使用安装在默认 R 库中的包。 更常见的做法，R 解决方案将通过在 R 代码中，指定的文件路径引用用户库，但不是建议这样做用于生产。

因此，它是数据库管理员或其他服务器上的管理员，以确保上是否安装了所有所需的程序包的任务 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例。 如果你没有管理权限的计算机上承载 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]  实例，你可以向管理员若要了解如何安装 R 包，提供并提供对其中可以获取包请求的用户的安全包存储库的访问。 本部分提供该信息。 

> [!TIP]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 提供用于安装和管理让数据库管理员和数据科学家更大的自由度和控制对包使用情况和安装的 R 包的新功能。 有关详细信息，请参阅 [for SQL Server 的 R 包管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。 

## <a name="installed-packages"></a>已安装的软件包
当你安装  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)],  ，默认情况下，R **基** 安装包，如 `stats` 和 `utils`, 以及 **RevoScaleR** 支持连接到的包 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 
> [!NOTE]  
>  默认情况下安装的包的列表，请参阅 [与 Microsoft R Open 安装包](https://mran.microsoft.com/rro/installed/)。  

 如果你需要从 CRAN 或另一个存储库的其他包，必须下载包并将其安装在你的工作站。  
  
 如果你需要在服务器的上下文中运行新的包，管理员必须安装它以及在服务器上。   
   
## <a name="where-and-how-to-get-new-packages"></a>获取新包的地方和方式  
 可以从多个来源获取 R 包，最广为人知的是 CRAN 和 Bioconductor。 R 语言官方站点 ([https://www.r-project.org/](https://www.r-project.org/)) 列出了很多这些资源。 许多包也发布到 GitHub，你可以从其获取源代码。 不过，你也可能已经从本公司的开发人员处获得了 R 包。  
  
 不管来源如何，提供的包必须采用 zip 文件格式以便进行安装。 此外，若要使用的包 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，一定要获取 Windows 二进制格式的压缩的文件。 （一些包可能不支持此格式。）有关的 zip 文件格式，以及如何创建 R 包内容的详细信息，我们建议本教程中，你可以从 R 项目站点的 PDF 格式下载该︰ [Freidrich Leisch︰ 创建 R 包](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)。 
  
 一般情况下，R 包可以轻松地从安装命令行而不事先情况下，将其下载如果计算机具有 Internet 访问权限。  通常这不是与服务器运行的情况 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 。  因此，若要将 R 包安装到计算机执行 **不** 都有 Internet 访问，必须下载中提前正确的压缩格式的包，然后将 zip 的文件复制到的计算机都可访问的文件夹。 
 
 以下主题介绍用于安装包脱机的两种方法︰ 

+ [创建脱机的程序包存储库使用 miniCRAN](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md)

  介绍如何使用 R 包 **miniCRAN** 若要创建的脱机存储库。 如果你需要将包安装到多个服务器和从单个位置管理存储库，则可能是最有效的方法。 
+ [从 Internet 中安装新的 R 包](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)

  包括用于安装包脱机通过手动复制压缩的文件的说明。   

## <a name="permissions-required-for-installing-r-packages"></a>安装 R 包所需的权限  
  
若要在运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的计算机上安装新的 R 包，你必须具有该计算机的管理权限。   

如果你没有这些权限，请联系管理员并提供要安装的包的相关信息。  
  

如果在用作 R 工作站的计算机上安装新的 R 包，并且该计算机将执行 **不** 具有的实例 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安装，仍需要到计算机的管理员权限才能安装包。 该包在安装后可以本地运行。  
 
> [!NOTE]
> 在 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], ，添加了新的数据库角色以支持的实例级别和数据库级别的包安装权限作用域。 有关详细信息，请参阅 [for SQL Server 的 R 包管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。
 

### <a name="location-of-default-r-library-location-for-r-services"></a>R Services 的默认 R 库位置的位置

如果你安装  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用默认实例，实例所使用的 R 包库位于 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例文件夹。 例如： 

+ 默认实例 _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ 命名实例 _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


你可以运行以下语句以验证默认库的当前实例的。 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

有关详细信息，请参阅 [确定的包安装在 SQL Server 上](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md)。

## <a name="managing-installed-packages"></a>管理已安装的程序包

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 提供用于安装和管理让数据库管理员和数据科学家更大的自由度和控制对包使用情况和安装的 R 包的新功能。 有关详细信息，请参阅 [for SQL Server 的 R 包管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。 

如果你使用的 SQL Server 2106 R 服务，新的程序包管理功能不可用在此时间。 在此期间，你可以使用以下选项用于确定哪些包安装在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机，请使用这些选项之一︰

+ 如果你具有对文件夹的权限，请查看默认库。
+ 运行 R 命令以列出 R_SERVICES 库位置中的包中的命令
+ 实例上使用存储的过程如下所示︰
   ```SQL
   EXECUTE sp_execute_external_script  @language=N'R'  
        ,@script = N'str(OutputDataSet);  
        packagematrix <- installed.packages();  
        NameOnly <- packagematrix[,1];  
        OutputDataSet <- as.data.frame(NameOnly);'  
        ,@input_data_1 = N'SELECT 1 as col'  
        WITH RESULT SETS ((PackageName nvarchar(250) ))   
   ```


 ## <a name="see-also"></a>另请参阅  
 [管理和监视 R 解决方案](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  