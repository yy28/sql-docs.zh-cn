---
title: "在 SQL Server 上安装其他 R 包 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: adc0e5fc229547632759c5702e98d87f4b71cbb3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="install-additional-r-packages-on-sql-server"></a>在 SQL Server 上安装其他 R 包
本主题介绍了如何在能够访问 Internet 的计算机上将新的 R 包安装到 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 实例。

## <a name="1-locate-the-windows-binaries-in-zip-file-format"></a>1.找到采用 ZIP 文件格式的 Windows 二进制文件

许多平台都支持 R 包。 你必须确保你要安装的包具有适用于 Windows 平台的二进制格式。 否则，下载的包将不会工作。

例如，若要获取 Bioconductor 提供的 [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) 包，请执行以下操作：  
  
1.  在“包存档”列表中，查找“Windows 二进制文件”版本。  
  
2.  右键单击 .ZIP 文件的链接，然后选择“将目标另存为”。    
  
3.  导航到存储 zip 包的本地文件夹，然后单击“保存”。   
  
 此过程将创建包的本地副本。 然后，你可以安装包，或者将压缩的包复制到不能访问 Internet 的服务器上。  
  
  
## <a name="2-open-the-default-r-package-library-for-sql-server-r-services"></a>2.打开 SQL Server R Services 的默认 R 包库 

在已安装了与 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 关联的 R 包的服务器上导航到该文件夹。 请务必将包安装到与当前实例关联的默认库。 

有关如何查找此库的说明，请参阅[安装和管理 R 包](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)。

   对于你将在其中运行包的每个实例，都必须安装包的单独副本。 当前，无法在各个实例之间共享包。
     
  
## <a name="3-open-an-administrative-command-prompt"></a>3.打开管理命令提示符 

以管理员身份打开 R。  你还可以使用 Windows 命令 p,ropt 或使用 R 实用工具之一执行此操作。
  
### <a name="using-the-windows-command-prompt"></a>使用 Windows 命令提示符 

1. 以管理员身份打开 Windows 命令提示符，然后导航到 RTerm.Exe 或 RGui.exe 文件所在目录。  
  
    进行默认安装时，该目录为 R **\bin** 。 例如，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，R 工具位于以下位置： 

    **默认实例**

     `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 
 
     **命名实例**
   
     `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`  
  
2. 运行 **R.Exe**。  
  
### <a name="using-the-r-command-line-utilities"></a>使用 R 命令行实用工具。 
  
1. 使用 Windows 资源管理器导航到包含 R 工具的目录。  
  
2. 右键单击 **RGui.exe** 或 **RTerm.exe**，然后选择“以管理员身份运行”。  
## <a name="4-install-the-package"></a>4.安装包

用来安装包的 R 命令取决于你是从 Internet 获取该包，还是从本地压缩文件获取该包。  
  
### <a name="install-package-from-internet"></a>从 Internet 安装包  
  
1.  通常，你使用以下命令来从 CRAN 或某个镜像站点安装新包。  
  
    ```  
    install.packages("target_package_name")  
    ```
    
    请注意，包名称必须使用双引号。

2.  若要指定应当在其中安装包的库，请使用类似于以下内容的命令来设置库位置：
    
    ```  
    lib.SQL <- "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\R_SERVICES\\library"    
    ```

    请注意，对于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，当前仅允许使用一个包库。 不要将包安装到用户库，否则你将无法从 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 运行包。   
     
3.  定义库位置之后，可使用以下语句将常用的 e1070 包安装到 R Services 使用的包库中。  
  
    ```  
    install.packages("e1071", lib = lib.SQL)  
    ```  
  
4.  系统会要求你提供从其获取包的镜像站点。 选择适合你所在位置的任何镜像站点。  
  
    如需当前 CRAN 镜像的列表，请查看 [此站点](https://cran.r-project.org/mirrors.html)。  
  
    > [!TIP]  
    >  为了避免每次添加新包都必须选择镜像站点，可将 R 开发环境配置为始终使用相同的存储库。  
    >   
    >  为此，请编辑全局 R 设置文件 .Rprofile，添加以下行：  
    >   
    >  `options(repos=structure(c(CRAN="<mirror site URL>")))`  
    >   
    >  如需首选项以及 R 运行时启动时所加载的其他文件的详细信息，请在 R 控制台中运行以下命令：  
    >   
    >  `?Startup`  
  
5.  如果目标包依赖于其他包，R 安装程序会自动下载并安装这些包。  
  
### <a name="manual-package-installation-or-installing-on-computer-with-no-internet-access"></a>手动安装包，或者在不能访问 Internet 的计算机上安装 

1. 如果你要安装的包具有依赖项，请提前获取所需的包并将它们添加到包含其他包压缩文件的文件夹中。

    > [!TIP]
    > 
    > 如果你需要支持频率的 R 包脱机安装，我们建议你使用 [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) 包设置一个本地存储库。  
  
2.  在 R 命令提示符下键入以下命令，以指定要安装的包的路径和名称：  
   
    ```  
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)  
    ``` 
     
    该命令从本地 zip 文件中提取 R 包（假定你已将副本保存在目录 `C:\Temp\Downloaded packages`中），并将包（及其依赖项）安装到本地计算机的 R 库中。  
  
3.  如果你之前修改了计算机上的 R 环境，则应当确保 R 环境变量 `.libPath` 仅使用一个路径，该路径应指向实例的 R_SERVICES 文件夹。  
  
> [!NOTE]
> 如果除了 SQL Server R Services 之外，你还安装了 Microsoft R Server（独立），则你的计算机将具有包含所有 R 工具和库的单独的 R 安装。 安装到 R_SERVER library 库的包仅可由 Microsoft R Server 使用，无法通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进行访问。  
> 
>  安装要在 SQL Server 中使用的包时，请务必使用 R_SERVICES 库。

  
## <a name="see-also"></a>另请参阅  
 [设置 SQL Server R Services（数据库内）](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  

