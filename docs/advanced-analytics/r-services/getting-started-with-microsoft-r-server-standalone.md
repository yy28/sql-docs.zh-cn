---
title: "Microsoft R Server（独立版）入门 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 57870cd1f1a84eb756314736a9a6cef9c574093b
ms.lasthandoff: 04/11/2017

---
# <a name="getting-started-with-microsoft-r-server-standalone"></a>Microsoft R Server（独立版）入门
  Microsoft R Server（独立版）可帮助将流行的开源 R 语言引入企业，以实现高性能分析解决方案以及与其他业务应用程序的集成。  

  
## <a name="install-microsoft-r-server"></a>安装 Microsoft R Server 

如何安装 Microsoft R Server 取决于你的应用程序中是否需要使用 SQL Server 数据。 如果需要，则应当使用 SQL Server 安装程序进行安装。 如果不使用 SQL Server 数据，或者不需要在数据库中运行 R 代码，则可以使用 SQL Server 安装程序，也可以使用新的独立安装程序。
 
 
+ 通过 SQL Server 安装程序安装 Microsoft R Server（独立版）。 将为 R Server 创建 R 二进制文件的一个单独实例，并且将通过 SQL Server Enterprise Edition 支持策略对实例进行许可。 有关详细信息，请参阅[创建独立的 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)。  

+ 使用新的独立版 Windows 安装程序创建 Microsoft R Server 的全新实例，该实例使用 Microsoft Modern Software Lifecycle 支持策略。 有关详细信息，请参阅[运行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。

+ 如果你有想要升级的现有 R Server（独立版）或 R Services 实例，则还必须下载并运行基于 Windows 的安装程序进行更新。 有关详细信息，请参阅[运行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。
  
## <a name="install-additional-r-tools"></a>安装其他 R 工具  

 我们建议你使用免费的 [Microsoft R 客户端](http://aka.ms/rclient/download)（下载）。  

 你还可以使用你喜欢的 R 开发环境来为 SQL Server R Services 或 Microsoft R Server 开发解决方案。 有关详细信息，请参阅[安装或配置 R 工具](../../advanced-analytics/r-services/setup-or-configure-r-tools.md)。 
 

### <a name="location-of-r-server-binaries"></a>R Server 二进制文件的位置

你用来安装 Microsoft R Server 的方法不同，默认位置也不同。 在开始使用你最喜欢的开发环境之前，请验证你将 R 库安装在了哪里：

+ 使用新的 Windows 安装程序安装的 Microsoft R Server

  `C:\Program Files\Microsoft\R Server\R_SERVER`

+ 通过 SQL Server 安装程序安装的 R Server（独立版）

  `C:\Program Files\Microsoft SQL Server\130\R_SERVER`

+ R Services (数据库中)

  `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`
      
## <a name="start-using-r-on-microsoft-r-server"></a>开始在 Microsoft R Server 上使用 R  

 在安装服务器组件并配置 R IDE 来使用 R Server 二进制文件之后，你可以开始使用新的 API（例如 RevoScaleR 包、MicrosoftML 和 olapR）来开发解决方案。
    
要开始使用 R Server，请参阅 MSDN 库中的以下指南：[R Server - 入门](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node)   
  
-   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started)：探究包含可分发的分析函数的这一集合，这些函数可提高 R 解决方案的性能和可伸缩性。 包括许多最流行的 R 建模包的可并行化版本，例如 K-均值聚类、决策树和决策林以及用于数据操作的工具。 有关详细信息，请参阅[通过 25 个函数探究 R 和 ScaleR](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started-tutorial)  
    
- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx)：MicrosoftML 包是由 Microsoft 开发的一组可快速运行且可伸缩的新的机器学习算法和转换。 有关详细信息，请参阅 [MicrosoftML 函数](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)。
  


  
## <a name="see-also"></a>另请参阅  
 [SQL Server R 服务入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  

