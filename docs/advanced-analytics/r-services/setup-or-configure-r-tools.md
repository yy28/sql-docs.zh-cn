---
title: "设置或配置 R 工具 | Microsoft Docs"
ms.custom: ""
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# 设置或配置 R 工具
  Microsoft R Server 提供的基的所有 R 库、 缩放 R 包和需要用于开发和测试 R 代码的标准 R 工具。 但是，如果你想要使用专用的 R 开发环境，有几个可用，包括许多免费工具。  
  
## <a name="basic-r-tools"></a>基本 R 工具  
 由于所有标准 R 工具中的 Microsoft R Server 安装不需要其他工具都将纳入 *基本安装* 的 R 安装默认情况下。

-   **RTerm**︰ 用于运行 R 脚本的命令行工具 
  
-   **RGui.exe**:。 的简单交互式编辑器命令行自变量都相同的 RGui.exe 和 RTerm。 
  
-   **RScript**︰ 命令行工具用于运行 R 脚本在批处理模式下。  

默认情况下，在下列文件夹中安装这些工具︰
- SQL Server 2016: `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin\x64`  
- SQL Server vNext: `C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`  

> [!TIP]  
>  需要更多帮助？ 可以在安装程序文件夹中找到 R 工具文档︰ `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` 并在 `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual`。  
>   
>  或者，只需打开 **RGui**, ，单击 **帮助**, ，然后选择其中一个选项。  

## <a name="microsoft-r-client"></a>Microsoft R Client

Microsoft R 客户端是一个免费下载，使你可以开发在 Microsoft R Server 或 SQL Server R Services 可以轻松运行的 R 解决方案。

通常你安装不同的 R 开发环境，例如 R Tools for Visual Studio 或 RStudio，，，然后指定 Microsoft R 客户端用作 R 可执行文件。 这样，可以完全访问权限 RevoScaleR 包和 Microsoft R Server 的其他功能。

你可以使用熟悉的工具，如 RGui 和 RTerm 运行脚本或编写和执行即席 R 代码。

[安装 Microsoft R 客户端](https://msdn.microsoft.com/microsoft-r/r-client-install)
  
##  <a name="a-namebkmkrtoolsa-r-tools-for-visual-studio"></a> R Tools for Visual Studio  

 为方便起见，在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库，请考虑使用 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 作为开发环境。 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 可用的加载项为适用于所有版本的 Visual Studio 的 Visual Studio。 Visual Studio 还提供对 Python 和 F # 集成的支持。  

有关详细信息，请参阅 [VisualStudio.com](https://www.visualstudio.com/vs/rtvs/)。

 本部分介绍如何安装 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 使用免费社区版的 Visual Studio。  
  
#### <a name="install-visual-studio"></a>安装 Visual Studio  
  
1.  Visual Studio 的免费的社区版是可供从该页下载︰ [Visual Studio Community](http://visualstudio.com/products/visual-studio-community-vs.aspx)  
  
2.  下载完成后，单击 **运行** ，然后选择要安装的组件。  
  
     如果你执行自定义安装程序，请注意，Microsoft Web Developer 组件需要。  
  
3.  选择 **常规** 暂时设置。 当你安装 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], ，你必须 toption 若要更改为 R 开发自定义布局。  

#### <a name="add-the-r-tools"></a>添加 R 工具

安装 Visual Studio 后，可以使用 R、 Python 和很多其他语言通过扩展 **选项** 菜单。

4. 从菜单栏中，单击工具，然后选择 **扩展和更新**。

5. 安装结束时，接近 R 工具将检测的 R 运行时，会在计算机上可用询问你是否要更改你的开发环境的 Microsoft R 客户端的 Microsoft R Server 或 R 运行时使用 R 运行时的版本。

如果安装程序未检测到你想要使用的 R Server 运行时，你可以手动更改在任何时候通过使用 **选项** 菜单。 有关详细信息，请参阅 [配置您 IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide)。

## <a name="rstudio"></a>RStudio

如果想要使用 RStudio，执行这些附加步骤来使用 RevoScaleR 库︰
- 安装 Microsoft R Server 或 Microsoft R 客户端，以获得所需的包和库。
- 更新要使用相应的 R 运行时你 R 路径。

有关详细信息，请参阅 [配置您 IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide)。


## <a name="see-also"></a>另请参阅  
 [创建 a Standalone R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [开始使用 Microsoft R Server &#40;独立 &#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  