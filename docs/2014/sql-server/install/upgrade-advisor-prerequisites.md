---
title: 升级顾问先决条件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
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
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5875ad2268e14d6bbe276ea437c5ee201867105e
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632772"
---
# <a name="upgrade-advisor-prerequisites"></a>升级顾问必备组件
  本主题介绍升级顾问的必备组件。  
  
## <a name="prerequisites"></a>先决条件  
 安装和运行升级顾问的必备组件如下：  
  
-   [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] SP1、[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]（最低为 SP2 版）、Windows 7 或 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] R2。  
  
-   Windows Installer 4.5。 你可以从[Windows Installer](https://www.microsoft.com/download/details.aspx?id=8483)网站安装 Windows Installer。  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]（最低为 .NET Framework 4）。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 产品媒体上提供，也可从[SDK、可再发行组件和 Service Pack 下载](https://go.microsoft.com/fwlink/?LinkId=48882)网站获得。  
  
    -   若要从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 介质安装 .NET Framework 4，请找到磁盘驱动器的根目录。 然后双击 \redist 文件夹，再双击 DotNetFrameworks 文件夹，然后运行 dotNetFx40_Full_x86_x64.exe（对于 32 位和 64 位操作系统）。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom 是安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 升级顾问的必备组件，并且不是由升级顾问安装程序安装的。 安装程序需要从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能包下载并安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom。  
  
## <a name="see-also"></a>另请参阅  
 [如何安装升级顾问](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md)  
  
  
