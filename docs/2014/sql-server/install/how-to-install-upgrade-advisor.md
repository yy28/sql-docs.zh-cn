---
title: 如何：安装升级顾问 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0de86b9690f0647803938218ce566508662da20e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094922"
---
# <a name="how-to-install-upgrade-advisor"></a>如何安装升级顾问
  升级顾问支持对除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之外的所有受支持组件进行远程分析。 如果不打算扫描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例，则可在能够连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的任何计算机上安装升级顾问。 计算机还必须满足升级顾问的前提条件。 如果要扫描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]实例，则必须在报表服务器上安装升级顾问。  
  
 有关详细信息，请参阅[安装升级顾问](../../../2014/sql-server/install/installing-upgrade-advisor.md)。  
  
### <a name="to-install-upgrade-advisor"></a>安装升级顾问  
  
1.  使用以下方法之一开始安装：  
  
    -   如果要从[!INCLUDE[msCoName](../../includes/msconame-md.md)]网站安装，请单击 "**下载**" 链接，然后单击 "**运行**" 按钮开始安装。  
  
    -   如果要从产品媒体进行安装，请打开 "再**发行**" 文件夹，打开 "**升级顾问**" 文件夹，然后双击 " **sqlua.msi**"。  
  
    > [!NOTE]  
    >  升级顾问要求 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4。 如果该软件未安装，或者如果安装的是预发行版本，则将出现一条错误消息。 请卸载 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的所有早期版本，然后安装最新版本的 .NET Framework 4。  
    >   
    >  ScriptDom 是安装[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]升级顾问的必备组件，并且不是由升级顾问安装程序安装的。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 安装程序[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]需要从[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]功能包下载和安装 ScriptDom。  
  
2.  在 "**欢迎使用升级[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]顾问安装程序**" 页上，单击 "**下一步**"。  
  
3.  在 "**许可协议**" 页上，阅读许可协议。 如果同意，请选择 **"我接受许可协议"** ，然后单击 "**下一步**"。  
  
4.  在 "**注册信息**" 页上，输入您的姓名和公司。  
  
5.  在 "**功能选择**" 页上，查看 "**安装路径**" 值。 如有必要，请使用 "**浏览**" 按钮更改位置。 单击“下一步”  。  
  
6.  在 "**准备安装程序"** 页上，单击 "**安装**" 以安装升级顾问。  
  
7.  单击“完成”**** 以退出向导。  
  
## <a name="see-also"></a>另请参阅  
 [升级顾问必备组件](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
