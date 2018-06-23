---
title: 安装 SQL Server 2014 服务更新 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c7601914ed32def54b153282a90b51629b1380b6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129726"
---
# <a name="install-sql-server-2014-servicing-updates"></a>安装 SQL Server 2014 服务更新
  本主题提供了有关为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安装更新的信息。 本节提供有关以下方面的信息：  
  
-   在全新安装期间为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装更新  
  
-   在已安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后为其安装更新  
  
 我们建议客户及时评估和安装最新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新，以便确保系统是最新的并且具有最近的安全更新。  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-during-a-new-installation"></a>在全新安装期间为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装更新  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将最新的产品更新集成到主产品安装中，以便可以同时安装主产品及其适用的更新。 产品更新可以从以下位置搜索适用的更新：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
-   Windows Server Update Services (WSUS)  
  
-   本地文件夹  
  
-   网络共享  
  
 在找到最新版本的适用更新后，安装程序将下载这些更新并将其与当前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装进程集成在一起。 产品更新可包括累积更新、Service Pack 或者 Service Pack 连同累积更新。 产品更新功能是扩展名为[Slipstream 功能](http://go.microsoft.com/fwlink/?LinkId=219945)，中提供的[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]PCU1。  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-after-it-has-already-been-installed"></a>在已安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后为其安装更新  
 已安装实例上[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，我们建议你应用所有可用的更新： 常规分发发布 (GDR-安全 / 关键更新)，Service Pack (SP)，以及最新可用累积更新 (CU)。  
  
 根据服务版本的类型，通过 Microsoft Update (MU)、 Microsoft Download Center，和/或客户支持服务修补程序服务器提供了 SQL Server 更新。 通过 Microsoft 更新 （以便能够查看你需要选择加入到 MU 通过 Windows 更新控制面板中的这些更新） 自动提供的 SQL Server 的安全和重要更新。 Service Pack 以及下载中心下载可选/重要事项是 MU 上可用。 累积更新是 Microsoft 修补程序下载服务器 CU 知识库文章中提供上可用。  
  
## <a name="see-also"></a>请参阅  
 [从安装向导安装 SQL Server 2014&#40;安装程序&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 [将功能添加到的 SQL Server 2014 实例&#40;安装程序&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [删除 SQL Server 2014 安装](repair-a-failed-sql-server-installation.md)  
  
  