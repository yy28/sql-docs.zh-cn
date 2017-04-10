---
title: "设置数据科学客户端 | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# 设置数据科学客户端
  通过安装 **R Services（数据库内）**配置 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的实例后，需要设置 R 开发环境，该环境能够连接用于远程执行和部署的服务器。 
  
  客户端环境应包括 Microsoft R Open，以及支持在 SQL Server 上分布式执行 R 的其他 RevoScaleR 包。  可以通过以下几种方法安装这些包：
  
+ 安装 [Microsoft R Client](http://aka.ms/rclient/download)。
+ 安装 Microsoft R Server。 可以从 SQL Server 安装程序或从独立安装程序获取 Microsoft R Server。 有关详细信息，请参阅[创建 R Server（独立版）](../../advanced-analytics/r-services/create-a-standalone-r-server.md)或 [R Server 简介](https://msdnstage.redmond.corp.microsoft.com/en-us/microsoft-r/rserver?branch=r-server-nov16-dev)。

 若要深入了解如何使用 Microsoft R Client 连接使用 ScaleR 包的 SQL Server，请参阅 [ScaleR 入门](https://msdn.microsoft.com/microsoft-r/scaler-getting-started#)。  
  
 有关如何连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例以远程执行 R 代码的详细演练，请参阅本教程：[对数据科学的深入探讨：使用 RevoScaleR 包](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)。  
  
## <a name="see-also"></a>另请参阅  
 [设置 SQL Server R Services（数据库内）](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  