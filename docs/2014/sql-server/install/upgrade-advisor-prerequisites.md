---
title: 升级顾问先决条件 |Microsoft 文档
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
- requirements [Upgrade Advisor]
- software [Upgrade Advisor]
- system requirements [Upgrade Advisor]
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, prerequisites
- prerequisites [Upgrade Advisor]
- Upgrade Advisor [SQL Server], prerequisites
ms.assetid: d21a39e5-5f81-4096-a7dd-f244e4779992
caps.latest.revision: 60
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7fb8f505610607052c12c68e910185a2a5e48f16
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126227"
---
# <a name="upgrade-advisor-prerequisites"></a>升级顾问必备组件
  本主题介绍升级顾问的必备组件。  
  
## <a name="prerequisites"></a>必要條件  
 安装和运行升级顾问的必备组件如下：  
  
-   [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] SP1、[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]（最低为 SP2 版）、Windows 7 或 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] R2。  
  
-   Windows Installer 4.5。 你可以安装 Windows Installer 从[Windows 安装程序网站](http://go.microsoft.com/fwlink/?LinkId=49112)。  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]（最低为 .NET Framework 4）。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]位于[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]产品媒体中，并从[SDK，可再发行组件和 service pack 下载网站](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
    -   若要从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 介质安装 .NET Framework 4，请找到磁盘驱动器的根目录。 然后双击 \redist 文件夹，再双击 DotNetFrameworks 文件夹，然后运行 dotNetFx40_Full_x86_x64.exe（对于 32 位和 64 位操作系统）。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom 是安装的先决条件[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]升级顾问，并不会安装升级顾问安装程序。 安装程序要求您下载并安装[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]从 ScriptDom[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]功能包。  
  
## <a name="see-also"></a>请参阅  
 [如何： 安装升级顾问](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md)  
  
  