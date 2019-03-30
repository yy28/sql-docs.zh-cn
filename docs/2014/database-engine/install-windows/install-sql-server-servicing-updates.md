---
title: 安装 SQL Server 2014 服务更新 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07f438f86a22b866351a0b83ee7634338f3ad2cd
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657841"
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
  
 在找到最新版本的适用更新后，安装程序将下载这些更新并将其与当前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装进程集成在一起。 产品更新可包括累积更新、Service Pack 或者 Service Pack 连同累积更新。 产品更新功能是的扩展[补充功能](https://go.microsoft.com/fwlink/?LinkId=219945)中[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]PCU1。  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-after-it-has-already-been-installed"></a>在已安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后为其安装更新  
 已安装实例上[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，我们建议你应用所有可用的更新：常规分发发布 (GDR-关键安全/更新)、 Service Pack (SP)，以及最新可用累积更新 (CU)。  
  
 根据服务发布的类型，SQL Server 更新均可通过 Microsoft Update (MU)、 Microsoft 下载中心，和/或客户支持服务修补程序服务器。 SQL Server 的安全和关键更新自动提供的 Microsoft 更新 （以便能够看到这些更新需要若要选择加入 mu 通过 Windows Update 控制面板中）。 可选/重要以及下载中心下载 Service Pack 是 MU 上可用。 CU 知识库文章中提供的 Microsoft 修补程序下载服务器上提供了累积更新。  
  
## <a name="see-also"></a>请参阅  
 [从安装向导安装 SQL Server 2014&#40;安装程序&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 [从命令提示符安装更新](installing-updates-from-the-command-prompt.md)[到 SQL Server 2014 实例添加功能&#40;安装程序&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [删除 SQL Server 2014 安装](repair-a-failed-sql-server-installation.md)  
  
  
