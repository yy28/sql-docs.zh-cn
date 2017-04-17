---
title: "设置数据科学客户端 | Microsoft Docs"
ms.custom: 
ms.date: 02/10/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 52f1962389a4eab48efc5fa1184990991511a8bd
ms.lasthandoff: 04/11/2017

---
# <a name="set-up--a-data-science-client"></a>Set Up  a Data Science Client
  通过安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] R Services（数据库内） **配置**的实例后，需要设置 R 开发环境，该环境能够连接用于远程执行和部署的服务器。 
  
  此环境必须包括 ScaleR 包，并可以选择包括客户端开发环境。
  
 ## <a name="where-to-get-scaler"></a>从何处获取 ScaleR 
  
  客户端环境必须包括 Microsoft R Open，以及支持在 SQL Server 上分布式执行 R 的其他 RevoScaleR 包。  可以通过以下几种方法安装这些包：
  
+ 安装 [Microsoft R Client](http://aka.ms/rclient/download)。 此处提供了其他安装说明：[Microsoft R 客户端入门](https://msdn.microsoft.com/microsoft-r/r-client-get-started)
+ 安装 Microsoft R Server。 可以从 SQL Server 安装程序获取 Microsoft R Server，也可以使用新的独立 Windows 安装程序。 有关详细信息，请参阅[创建独立的 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md) 和 [R Server 简介](https://msdn.microsoft.com/microsoft-r/rserver)。

如果你有 R Server 许可协议，我们建议使用 Microsoft R Server（独立版），以避免在 R 处理线程和内存中数据时遇到限制。


## <a name="how-to-set-up-the-r-development-environment"></a>如何设置 R 开发环境

可以使用所选的任何与 Windows 兼容的 R 开发环境。 

+ 针对 Visual Studio 的 R 工具支持与 Microsoft R Open 集成
+ RStudio 是常用的免费环境  

安装之后，将需要重新配置环境以在默认情况下使用 Microsoft R Open 库，否则你将无法访问 ScaleR 库。 有关详细信息，请参阅 [Microsoft R 客户端入门](http://msdn.microsoft.com/microsoft-r/r-client-get-started)。
 
## <a name="more-resources"></a>更多资源
  
 有关如何连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例以远程执行 R 代码的详细演练，请参阅本教程： [对数据科学的深入探讨：使用 RevoScaleR 包](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)。  
 

若要开始将 Microsoft R 客户端和 ScaleR 包与 SQL Server 配合使用，请参阅 [ScaleR 入门](https://msdn.microsoft.com/microsoft-r/scaler-getting-started#)。  
  
## <a name="see-also"></a>另请参阅  
 [设置 SQL Server R Services（数据库内）](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  

