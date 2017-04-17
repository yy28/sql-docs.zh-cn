---
title: R Services | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 12/20/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0faff61dffddad30d6f9d16bec4e3c94e6673b26
ms.lasthandoff: 04/11/2017

---
# <a name="r-services"></a>R Services
  Microsoft R Services 提供两个服务器平台，用于将热门的开放源代码 R 语言与业务应用程序集成，这两个平台分别为：**SQL Server R Services（数据库内）**（用于与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 集成）和 **Microsoft R Server**（用于在 Windows 和 Linux 服务器上进行企业级 R 部署）。  
  
-   **R Services（数据库内）**  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的目标是基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 平台和相关服务快速开发、部署和实施 R 解决方案。  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 通过允许 R 作为数据库在同一台计算机上运行，实现对数据进行计算。 它包含在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程外运行的数据库服务，并与 R 运行时安全通信。 用户可以设定 R 模型定型、生成 R 图形、执行评分，并在 R 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之间轻松移动数据。 负责测试和开发解决方案的数据科学家可以从远程开发计算机与服务器通信，以便在服务器上运行 R 代码，并通过在存储过程中嵌入对 R 的调用，将已完成的解决方案部署到 SQL Server。  
  
     此下载包括开放源代码 R 语言以及 ScaleR 的分发（后者是一套高性能的可缩放 R 包）。 它还包含提供程序，可以更便捷地连接所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技术。  
  
     有关详细信息，请参阅 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)。 有关示例方案，请参阅 [SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)。  
  
-   **Microsoft R Server**  
  
     此独立服务器系统支持在多个平台上部署使用多个企业数据源（包括 Linux、Hadoop 和 Teradata）的分布式的可缩放 R 解决方案。  
  
     有关详细信息，请参阅 [Microsoft R Server (MSDN)](https://msdn.microsoft.com/microsoft-r/index)。  
  
## <a name="related-technologies"></a>相关技术  
 Microsoft 对开放源代码 R 语言生态系统提供广泛的支持，包括工具、提供程序、增强的 R 程序包和集成的开发环境。  
  
-   **用于 Visual Studio 的 R 工具**  
  
     Visual Studio 为 R 语言提供完整的开发环境。 该插件包含编辑器、交互式窗口、绘图、调试器等等。 你可以通过 R.NET 和 rClr 等开放源代码库从 R 使用 .NET 语言或从 .NET 调用 R。  
  
     有关详细信息，请参阅 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)。  
  
-   **Azure 机器学习中的 R**  
  
     在 Azure 机器学习工作室中创建你自己的工作区，通过该工作区可访问超过 400 个预加载的 R 程序包。 生成模型并将其定型以作为 Web 服务部署，或编写自定义脚本以转换数据。 创建你自己的 R 程序包并将其上载到 Azure 以作为自定义模块运行，然后将解决方案发布到 [机器学习应用商店](http://datamarket.azure.com/browse/data?category=machine-learning)。  
  
     有关详细信息，请参阅[使用 R 扩展试验](https://docs.microsoft.com/azure/machine-learning/machine-learning-extend-your-experiment-with-r)和[在 Azure 机器学习中创作自定义 R 模块](https://docs.microsoft.com/azure/machine-learning/machine-learning-custom-r-modules)。  
  
-   **数据科学虚拟机**  
  
     用户可以在 Microsoft Azure 中部署 [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] 的预安装和预配置版本，这样就可以立即在云上轻松地开始使用数据浏览和建模，而无需在本地设置完整配置的系统。  
  
     Azure 应用商店包含多个支持数据科学的虚拟机：
     + **Microsoft 数据科学虚拟机**配置了 Microsoft R Server、Python（Anaconda 分发版）、Jupyter Notebook 服务器、Visual Studio Community Edition、Power BI Desktop、Azure SDK 和 SQL Server Express Edition。 
     + **Microsoft R Server 2016 for Linux** 包含最新版本的 R Server（版本 9.0.1）。 针对 CentOS 版本 7.2 和 Ubuntu 版本 16.04 提供单独的 VM。 
     + **R Server Only SQL Server 2016 Enterprise** 虚拟机包括 R Server 9.0.1 的独立安装程序，支持全新的现代软件生命周期授权模型。
 

## <a name="see-also"></a>另请参阅  
[SQL Server R 服务入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md) 

[Microsoft R Server 入门](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  

 [安装 SQL Server 数据库引擎](../../database-engine/install-windows/install-sql-server-database-engine.md)  
  
  

