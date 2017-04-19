---
title: "R Server（独立版）| Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/07/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: ca9e48f1-67b8-4905-9b78-56752d7a4e81
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bff45d6e7fed98bfa39ccd7d80cee0c957ccb9ad
ms.lasthandoff: 04/11/2017

---
# <a name="r-server-standalone"></a>R Server (Standalone)
  **Microsoft R Server（独立版）**是 Microsoft R Services 提供的企业级分析平台的一部分。  它通过提供支持、可伸缩性和安全性对 R 进行了扩展。 [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] 还通过添加并行和分块数据处理，解决开放源代码 R 的内存中限制，从而使用户能够分析企业级规模的数据和使用规模远超内存容量的数据。  
 
 你可以在多个平台上使用 Microsoft R Server。 有关详细信息，请参阅 MSDN 库中的以下资源：  

+ [Microsoft R Server 简介](https://msdn.microsoft.com/microsoft-r/rserver)
+ [R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)

你还可以将 Microsoft R Server 用作开发客户端，以获取创建可以部署到 SQL Server 的 R 解决方案时所需的 RevoScaleR 库和工具。
  
  
## <a name="how-to-get-microsoft-r-server"></a>如何获取 Microsoft R Server  
 
 有多个选项可用于安装 Microsoft R Server，具体取决于你是否需要使用 SQL Server 数据以及你希望以何频率获取更新：
 
+ **Microsoft R Server（独立版）**：如果你希望为企业 R 解决方案设置开发机器，请运行 SQL Server 安装向导并选择此选项。 你可以在本地在你安装独立实例的计算机上运行解决方案，也可以使用 SQL Server R Services 连接到 SQL Server 实例并以服务器作为计算上下文来运行解决方案。 

    安装 Microsoft R Server（独立版）时，将通过 SQL Server Enterprise Edition 支持策略对实例进行许可。 此选项提供较长时间的更新和客户支持，以及绑定到 SQL Server 发布计划的功能更新。 这可以确保你使用 Microsoft R Server 创建的应用程序始终与运行 R Services（数据库中）的 SQL Server 实例兼容。 有关详细信息，请参阅[创建独立的 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)。  
    
    不需要在已经安装了 SQL Server R Services 的计算机上安装 Microsoft R Server（独立版）。 

+ **采用 Modern Software Lifecycle 支持策略的 Microsoft R Server**：现在，你可以使用新的 Windows 安装程序来安装新的 Microsoft R Server 实例。 如果你不需要使用数据库中分析，或者希望使用 Microsoft Modern Software Lifecycle 策略较频繁地进行更新，请使用此选项安装 Microsoft R Server。 

    虽然此服务器版本的许可需要 SQL Server Enterprise 协议，但不会将你绑定到 SQL Server 发布周期。 这可以确保你较频繁地获得 R 的更新。有关此版本的 Microsoft R Server 的详细信息，请参阅[运行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。
 
    通过使用此安装程序，你还可以转换 SQL Server R Services 的现有实例，以将其绑定到 Microsoft Modern Software Lifecycle 支持策略并因此获得更频繁的更新。 若要执行更新，你需要具有兼容的现有安装。 有关详细信息，请参阅[使用 SqlBindR 升级 R Services 的实例](../../advanced-analytics/r-services/use-sqlbindr-exe-to-upgrade-an-instance-of-r-services.md)。
 
    
+ **具有 R Server 的 Azure 虚拟机**：Azure 应用商店中具有多个包含 R Server 的虚拟机映像。 要安装用于实施预测模型的服务器，最快的方法是创建新的 Azure 虚拟机。 某些映像附带了已配置的缩放和共享功能（以前称为 DeployR），这使得在应用程序内嵌入 R 分析以及将 R 与后端系统进行集成变得更为容易。 有关详细信息，请参阅[预配 R Server 虚拟机](../../advanced-analytics/r-services/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
有关 Microsoft R 的示例、教程和详细信息，请参阅 [Microsoft R 产品](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started)。   
  
## <a name="see-also"></a>另请参阅  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [使 R 成为本地和云中跨平台分析的企业标准](http://blogs.technet.com/b/machinelearning/archive/2016/01/12/making-r-the-enterprise-standard-for-cross-platform-analytics-both-on-premises-and-in-the-cloud.aspx)  
  
  

