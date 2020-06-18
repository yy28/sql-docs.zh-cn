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
ms.openlocfilehash: 0c36fbe634fbc2b17547f127290cfbaed6e745c7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932517"
---
# <a name="install-sql-server-2014-servicing-updates"></a>安装 SQL Server 2014 服务更新
  本主题提供了有关为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安装更新的信息。 本节提供有关以下方面的信息：  
  
-   在全新安装期间为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装更新  
  
-   在已安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后为其安装更新  
  
 我们建议客户及时评估和安装最新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新，以便确保系统是最新的并且具有最近的安全更新。  
  
## <a name="installing-updates-for-sscurrent-during-a-new-installation"></a>在全新安装期间为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装更新  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将最新的产品更新集成到主产品安装中，以便可以同时安装主产品及其适用的更新。 产品更新可以从以下位置搜索适用的更新：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
-   Windows Server Update Services (WSUS)  
  
-   本地文件夹  
  
-   网络共享  
  
 在找到最新版本的适用更新后，安装程序将下载这些更新并将其与当前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程集成在一起。 产品更新可包括累积更新、Service Pack 或者 Service Pack 连同累积更新。 产品更新功能是 PCU1 中提供的补充[功能](https://go.microsoft.com/fwlink/?LinkId=219945)的扩展 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 。  
  
## <a name="installing-updates-for-sscurrent-after-it-has-already-been-installed"></a>在已安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后为其安装更新  
 在的已安装实例上 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，我们建议你应用所有可用的更新：常规分发版本（GDR-安全/关键更新）、Service pack （SP）以及最新的可用累积更新（CU）。  
  
 根据服务发布的类型，可以通过 Microsoft 更新（MU）、Microsoft 下载中心和/或客户支持服务修补程序服务器提供 SQL Server 更新。 Microsoft 更新自动提供 SQL Server 的安全更新和关键更新（通过控制面板中的 Windows 更新，可以查看需要选择加入 MU 的这些更新）。 在 MU 上，Service Pack 可作为可选/重要下载和下载中心提供。 在 CU 知识库文章中提供的 Microsoft 修补程序下载服务器上提供了累积更新。  
  
## <a name="see-also"></a>另请参阅  
 [从安装向导安装 SQL Server 2014 &#40;安装程序&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 [从命令提示符安装更新](installing-updates-from-the-command-prompt.md)会[将功能添加到 SQL Server 2014 &#40;安装程序的实例&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [删除 SQL Server 2014 安装](repair-a-failed-sql-server-installation.md)  
  
  
