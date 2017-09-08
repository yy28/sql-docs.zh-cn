---
title: "安装和管理 R 包 | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ae30bfc42e42b69158dbba5a38b0bccbe93523b4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="installing-and-managing-r-packages"></a>安装和管理 R 包
 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中运行的任何 R 解决方案必须使用默认 R 库中安装的包。 更常见的情况是，R 解决方案通过在 R 代码中指定文件路径来引用用户库，但我们不建议在生产环境中使用这种做法。

因此，确保在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例上安装全部所需的包是服务器上数据库管理员和其他管理员的任务。 如果你在托管 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例的计算机上没有管理特权，可向管理员提供有关如何安装 R 包的信息，并提供用户可在其中获取所请求包的安全包存储库的访问权限。 本部分提供与此相关的信息。 

> [!TIP]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 提供了新的功能用于安装和管理 R 包，使数据库管理员和数据科研人员能够以更大的自由度和力度控制包的用法与设置。 有关详细信息，请参阅 [SQL Server 的 R 包管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。 

## <a name="installed-packages"></a>安装的包
安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 时，默认安装 R **基础**包（例如 `stats` 和 `utils`），以及用于支持与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立连接的 **RevoScaleR** 包。  
  
 
> [!NOTE]  
>  有关默认安装的包列表，请参阅 [Packages Installed with Microsoft R Open](https://mran.microsoft.com/rro/installed/)（连同 Microsoft R Open 一起安装的包）。  

 如果需要 CRAN 或另一存储库中的其他包，必须下载该包并将它安装在工作站上。  
  
 如果需要在服务器上下文中运行新包，管理员也必须将它安装在服务器上。   
   
## <a name="where-and-how-to-get-new-packages"></a>获取新包的地方和方式  
 可以从多个来源获取 R 包，最广为人知的是 CRAN 和 Bioconductor。 R 语言的官方站点 ([https://www.r-project.org/](https://www.r-project.org/)) 列出了许多这样的资源。 许多包也发布到 GitHub，你可以从其获取源代码。 不过，你也可能已经从本公司的开发人员处获得了 R 包。  
  
 不管来源如何，提供的包必须采用 zip 文件格式以便进行安装。 此外，若要对 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用包，请务必获取 Windows 二进制格式的压缩文件。 （某些包可能不支持此格式。）有关 zip 文件格式内容以及如何创建 R 包的详细信息，我们建议阅读以下教程（可以从 R 项目站点下载 PDF 格式的教程）：[Freidrich Leisch: Creating R Packages](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)（Freidrich Leisch：创建 R 包）。 
  
 一般情况下，如果计算机可以访问 Internet，则无需提前下载，就能轻松地从命令行安装 R 包。  通常，运行 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的服务器无法访问 Internet。  因此，若要将某个 R 包安装到**无法**访问 Internet 的计算机，必须提前下载采用适当压缩格式的包，然后将压缩文件复制到计算机可访问的文件夹中。 
 
 以下主题介绍了脱机安装包的两种方法： 

+ [Create an Offline Package Repository using miniCRAN](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md)（使用 miniCRAN 创建脱机包存储库）

  介绍如何使用 R 包 **miniCRAN** 创建脱机存储库。 如果需要将包安装到多个服务器并从单个位置管理存储库，则这可能是最有效的方法。 
+ [Install New R Packages from the Internet](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)（从 Internet 安装新的 R 包）

  提供有关通过手动复制压缩文件来脱机安装包的说明。   

## <a name="permissions-required-for-installing-r-packages"></a>安装 R 包所需的权限  
  
若要在运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的计算机上安装新 R 包，必须拥有该计算机的管理权限。   

如果你没有这些权限，请联系管理员并提供要安装的包的相关信息。  
  

如果要将新 R 包安装到用作 R 工作站的计算机上，而该计算机上**未**安装 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的实例，则你仍需要计算机管理权限才能安装该包。 该包在安装后可以本地运行。  
 
> [!NOTE]
> 在 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 中，已添加新的数据库角色来支持实例级别和数据库级别的包安装权限范围。 有关详细信息，请参阅 [SQL Server 的 R 包管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。
 

### <a name="location-of-default-r-library-location-for-r-services"></a>R Services 的默认 R 库位置

如果使用默认实例安装了 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，该实例使用的 R 包库位于 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例文件夹中。 例如： 

+ 默认实例 _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ 命名实例 _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


可以运行以下语句来验证 R.的当前实例的默认库。 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

有关详细信息，请参阅[确定要在 SQL Server 上安装的包](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md)。

## <a name="managing-installed-packages"></a>管理安装的包

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 提供了新的功能用于安装和管理 R 包，使数据库管理员和数据科研人员能够以更大的自由度和力度控制包的用法与设置。 有关详细信息，请参阅 [SQL Server 的 R 包管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。 

如果你正在使用 SQL Server 2106 R Services，新的包管理功能目前不可用。 同时，可以使用这些选项之一来确定 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机上安装了哪些包：

+ 查看默认库（如果对该文件夹拥有权限）。
+ 在 R 命令中运行某个命令列出位于 R_SERVICES 库位置的包
+ 在实例上使用如下所示的存储过程：
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

