---
title: "安装 SQL Server 2016 服务更新 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
caps.latest.revision: 13
ms.author: "mikeray"
manager: "jhubbard"
---
# 安装 SQL Server 2016 服务更新
  本主题提供了有关为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安装更新的信息。 本节提供有关以下方面的信息：  
  
-   在全新安装期间为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装更新  
  
-   在已安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后为其安装更新  
  
 我们建议客户及时评估和安装最新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新，以便确保系统是最新的并且具有最近的安全更新。  
  
## 在全新安装期间为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装更新  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将最新的产品更新集成到主产品安装中，以便可以同时安装主产品及其适用的更新。 产品更新可以从以下位置搜索适用的更新：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
-   Windows Server Update Services (WSUS)  
  
-   本地文件夹  
  
-   网络共享  
  
 在找到最新版本的适用更新后，安装程序将下载这些更新并将其与当前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装进程集成在一起。 产品更新可包括累积更新、Service Pack 或者 Service Pack 连同累积更新。  
  
## 在已安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后为其安装更新  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的已安装实例上，我们建议应用最新的安全更新和关键更新，包括常规分发发布 (GDR)、Service Pack (SP) 和累积更新 (CU)。 有关其他信息，请参阅 [2016 年 3 月针对 SQL Server 增量服务模式 (ISM) 的公告](http://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism/)。 
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新可通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新 (MU)、Windows Server Update Services (WSUS) 和 Microsoft 下载中心获得。 针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安全更新和关键更新通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新提供，并且能够通过控制面板中的 Windows Update 小程序查看您需要的选择进入 MU 的这些更新。  
  
 在您通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新接收某一更新时，它会以无人参与模式将所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能更新为最新版本。 如果您需要更多的灵活性或者没有 Internet 或 WSUS 访问，将需要从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 下载中心获取更新。  
  
## 另请参阅  
 [使用安装向导安装 SQL Server 2016（安装程序）](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)   
 [向 SQL Server 2016 的实例添加功能（安装程序）](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)   
 [修复失败的 SQL Server 2016 安装](../../database-engine/install-windows/repair-a-failed-sql-server-2016-installation.md)  
  
  