---
title: "在 SQL Server 上安装其他 R 包 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# 在 SQL Server 上安装其他 R 包
本主题介绍如何以将新的 R 包安装到的实例 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 有权访问 Internet 的计算机上。

## <a name="1-locate-the-windows-binaries-in-zip-file-format"></a>1.找到 Windows 二进制文件的 ZIP 文件格式

在许多平台上支持的 R 程序包。 你必须确保你想要安装的程序包具有适用于 Windows 平台的二进制格式。 否则下载的包将无法工作。

例如，若要获取 Bioconductor 提供的 [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) 包，请执行以下操作：  
  
1.  在 **包存档** 列表中，找到 **Windows 二进制文件** 版本。  
  
2.  右键单击 .ZIP 文件的链接，然后选择“将目标另存为”。    
  
3.  导航到存储 zip 包的本地文件夹，然后单击“保存”。   
  
 此过程将创建包的本地副本。 然后可以安装包，也可将压缩的包复制到的服务器，不能访问 Internet。  
  
  
## <a name="2-open-the-default-r-package-library-for-sql-server-r-services"></a>2.打开 SQL Server R Services 默认 R 包库 

导航到与关联的 R 包在服务器上的文件夹 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 已安装。 务必将包安装到当前实例相关联的默认库。 

有关如何查找此库的说明，请参阅 [安装和管理 R 包](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)。

   对于每个要在其中运行包的实例，你必须安装包的单独副本。 当前无法在实例之间共享包。
     
  
## <a name="3-open-an-administrative-command-prompt"></a>3.打开管理命令提示符 

以管理员身份打开 R。  通过使用 Windows 命令 p，ropt，或通过使用 R 实用工具之一时，可以执行此操作。
  
### <a name="using-the-windows-command-prompt"></a>使用 Windows 命令提示符 

1. 打开 Windows 命令提示符以管理员身份，并导航到 RTerm.Exe 或 RGui.exe 文件所在的目录。  
  
    进行默认安装时，该目录为 R **\bin** 。 例如，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，R 工具位于此处︰ 

    **默认实例**

     `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 
 
     **命名的实例**
   
     `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`  
  
2. 运行 **R.Exe**。  
  
### <a name="using-the-r-commandline-utilities"></a>使用 R 命令行实用工具。 
  
1. 使用 Windows 资源管理器导航到包含 R 工具的目录。  
  
2. 右键单击 **RGui.exe** 或 **RTerm.exe**, ，然后选择 **以管理员身份运行**。  
## <a name="4-install-the-package"></a>4.安装包

要安装包的 R 命令取决于是否得到包从 Internet 还是从本地 zip 文件。  
  
### <a name="install-package-from-internet"></a>从 Internet 安装包  
  
1.  一般情况下，你可以使用以下命令从 CRAN 或其中一个镜像站点中安装新的包。  
  
    ```  
    install.packages("target_package_name")  
    ```
    
    请注意，包名称必须使用双引号。

2.  若要指定应安装包的位置的库，使用类似此命令的命令设置库位置︰
    
    ```  
    lib.SQL <- "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\R_SERVICES\\library"    
    ```

    请注意，对于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 、 当前允许只有一个包库。 不将包安装到用户的库，或你将不能运行从包 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。   
     
3.  定义了库位置后，以下语句将常用 e1070 包安装到 R Services 使用的包库。  
  
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
  
### <a name="manual-package-installation-or-installing-on-computer-with-no-internet-access"></a>手动的包安装，或在没有 Internet 访问权限的计算机上安装 

1. 如果你想要安装的包具有依赖关系，将显示提前所需的包并将它们添加到文件夹中，使用压缩文件的其他包。

    > [!TIP]
    > 
    > 我们建议你设置本地存储库使用 [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) 如果你需要支持频繁脱机安装的 R 包。  
  
2.  在 R 命令提示符下键入以下命令，以指定要安装的包的路径和名称：  
   
    ```  
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)  
    ``` 
     
    此命令从其本地 zip 文件，假定副本保存在目录中提取 R 包 `C:\Temp\Downloaded packages`, ，并将 （包括其依赖项） 的包安装到本地计算机上的 R 库。  
  
3.  如果以前已修改的计算机上的 R 环境，则应确保 R 环境变量 `.libPath` 使用一个路径，指向 R_SERVICES 文件夹的实例。  
  
> [!NOTE]
> 如果已安装除了 SQL Server R Services 的 Microsoft R Server （独立版），则计算机将具有与所有 R 工具和库的单独安装的 R。 这些包安装到 R_SERVER 库仅由 Microsoft R Server 使用，不能由访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
> 
>  请务必在安装你想要使用 SQL Server 中的包时使用 R_SERVICES 库。

  
## <a name="see-also"></a>另请参阅  
 [设置 SQL Server R Services &#40; 数据库中 &#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  