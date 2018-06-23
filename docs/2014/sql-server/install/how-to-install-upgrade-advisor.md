---
title: 如何： 安装升级顾问 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b98a4b134025d22ad9d13ce9fa38a7e4f2605e0b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129603"
---
# <a name="how-to-install-upgrade-advisor"></a>如何安装升级顾问
  升级顾问支持对除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之外的所有受支持组件进行远程分析。 如果不打算扫描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例，则可在能够连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的任何计算机上安装升级顾问。 计算机还必须满足升级顾问的前提条件。 如果要扫描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]实例，则必须在报表服务器上安装升级顾问。  
  
 有关详细信息，请参阅[安装升级顾问](../../../2014/sql-server/install/installing-upgrade-advisor.md)。  
  
### <a name="to-install-upgrade-advisor"></a>安装升级顾问  
  
1.  使用以下方法之一开始安装：  
  
    -   如果要从安装[!INCLUDE[msCoName](../../includes/msconame-md.md)]Web 站点，请单击**下载**链接，然后单击**运行**按钮以开始安装。  
  
    -   如果要从产品媒体中安装，打开**redist**文件夹中，打开**升级顾问**文件夹，然后再双击**SQLUA.msi**。  
  
    > [!NOTE]  
    >  升级顾问要求 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4。 如果该软件未安装，或者如果安装的是预发行版本，则将出现一条错误消息。 请卸载 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的所有早期版本，然后安装最新版本的 .NET Framework 4。  
    >   
    >  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom 是安装的先决条件[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]升级顾问，并不会安装升级顾问安装程序。 安装程序要求您下载并安装[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]从 ScriptDom[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]功能包。  
  
2.  上**欢迎[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]升级顾问安装程序**页上，单击**下一步**。  
  
3.  上**许可协议**页上，阅读许可协议。 如果同意，请选中**我接受许可协议**，然后单击**下一步**。  
  
4.  上**注册信息**页上，输入名称和公司。  
  
5.  上**功能选择**页上，查看**安装路径**值。 如有必要，使用**浏览**按钮以更改位置。 单击“下一步” 。  
  
6.  上**准备好安装程序**页上，单击**安装**安装升级顾问。  
  
7.  单击 **“完成”** 退出向导。  
  
## <a name="see-also"></a>请参阅  
 [升级顾问先决条件](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  