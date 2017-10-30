---
title: "设置或配置 R 工具 | Microsoft Docs"
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3baf97a960d7e8f950bb6e9cd251550f4c4b942
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="setup-or-configure-r-tools"></a>设置或配置 R 工具
  Microsoft R Server 提供开发和测试 R 代码所需的所有基础 R 库、一套 ScaleR 包和标准的 R 工具。 但是，如果你想要使用专用的 R 开发环境，可以安装几个可用的专用环境，其中包括许多免费工具。  
  
## <a name="basic-r-tools"></a>基本 R 工具  
 Microsoft R Server 的安装中不需要额外的工具，因为默认已安装 R *基础安装*中包含的所有标准 R 工具。

-   **RTerm**：用于运行 R 脚本的命令行工具 
  
-   **RGui.exe**：适用于 R 的简单交互式编辑器。RGui.exe 和 RTerm 的命令行参数相同。 
  
-   **RScript**：用于以批处理模式运行 R 脚本的命令行工具。  

若要查找这些工具，请找到 R 库的位置。 根据你是只安装了 SQL Server R Services，还是同时安装了 R Server（独立版），此位置将有所不同。 有关详细信息，请参阅 [What is Installed and Where to Find R Packages](https://msdn.microsoft.com/library/mt695941(sql.130).aspx#Anchor_1)（安装的内容以及在何处找到 R 包）

然后查看文件夹 `..\R_SERVER\bin\x64`。  

> [!TIP]  
>  需要 R 工具的帮助？ 安装文件夹 `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` 以及 `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual` 中提供了文档。  
>   
>  或者，只需打开“RGui”，单击“帮助”，然后选择其中一个选项。  

## <a name="microsoft-r-client"></a>Microsoft R Client

Microsoft R Client 是一个免费下载的工具，让你开发可在 Microsoft R Server 或 SQL Server R Services 中轻松运行的 R 解决方案。 提供此选项的目的是帮助无法访问 R Server (Enterprise Edition) 的数据科研人员开发使用 ScaleR 的解决方案。 

如果你在其他 R 开发环境（例如，用于 Visual Studio 的 R 工具或 RStudio）中使用 ScaleR，必须指定将 Microsoft R Client 用作 R 可执行文件。 这样，你便拥有 RevoScaleR 包以及其他 Microsoft R Server 功能的完全访问权限，不过性能将受到限制。

还可以使用 R Client 中提供的工具（例如 RGui 和 RTerm）来运行脚本，或者编写和执行即席 R 代码。

[安装 Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-install)
  
##  <a name="bkmk_RTools"></a> 用于 Visual Studio 的 R 工具  

 为方便使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库，请考虑使用 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 作为开发环境。 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 是适用于 Visual Studio 的免费加载项，可在所有版本的 Visual Studio 中运行。 Visual Studio 还提供对 Python 和 F # 集成的支持。  

 有关安装说明，请参阅[如何安装 R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)。

> [!TIP]
> 在安装任何新包之前，请检查默认使用的 R 运行时。 否则，很有可能会将新 R 包安装到默认库位置，以后无法在 R Server 中找到这些包！


## <a name="rstudio"></a>RStudio

如果你偏好使用 RStudio，需要执行一些附加的步骤来使用 RevoScaleR 库：
- 安装 Microsoft R Server 或 Microsoft R Client 来获取所需的包和库。
- 更新 R 路径以使用 R Server 运行时。

有关详细信息，请参阅 [Configure Your IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide)（配置 IDE）。


## <a name="see-also"></a>另请参阅  
 [创建独立版 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [Microsoft R Server（独立版）入门](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  

