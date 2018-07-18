---
title: 软件维护服务的分析平台系统 |Microsoft Docs
description: 软件维护服务中 Analytics Platform System (APS)。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 79231b6e2867154bc4d826b83a0a4fd27487f438
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909797"
---
# <a name="software-servicing-in-analytics-platform-system"></a>在分析平台系统中的软件维护服务
本部分总结了服务的分析平台系统设备，包括 WSUS 和 Analytics Platform System 修补程序要求的软件。  
  
## <a name="Basics"></a>软件维护基础  
**WSUS:** 分析平台系统 appliance 需要进行配置以接收从 Windows Server Update Services (WSUS) 的更新。 这些更新包括设备软件的重要更改。 配置后，许多更新将自动安装，并不需要实际操作管理。 通常情况下，WSUS 更新配置期间[配置 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41; ](configure-windows-server-update-services-wsus.md)新设备安装过程中执行的步骤。 如果没有，可以稍后执行此配置步骤。 有关 WSUS 的信息，请参阅[WSUS 网站指南](http://go.microsoft.com/fwlink/?LinkId=202417)。  
  
**修补程序：** 此外，您可能需要应用 Analytics Platform System 修补程序。 一个*修补程序*是为特定客户来解决问题，分析平台系统软件创建的软件更新。 每个修补程序是安装特定于客户的问题的修补程序的可执行文件。 每个修补程序还包含 Windows、 SQL Server 和分析平台系统的所有以前发布的软件更新的累积。 如果你需要安装的修补程序，Microsoft 支持部门将提供您的修补程序和说明。  
  
**更新的作用域：** 将修补程序或服务包应用于分析平台系统必须使整个设备脱机。  
  
**SSIS 目标适配器和客户端工具：** 应用修补程序时，包括对 SSIS 目标适配器 MSI 的更改或 MSI 文件将更新在客户端工具 MSI **C:\PDWINST\ClientTools**在控制节点上的目录。 此修补程序不会自动安装组件从更新的 MSI 文件。 若要更新这些组件，客户必须卸载旧版本的组件，并从更新的 MSI 文件安装新版本。 卸载修补程序时，包括对 SSIS 目标适配器 MSI 的更改或客户端工具 MSI，这些组件的 MSI 文件将恢复到以前的版本。 若要还原到以前的版本这些组件，客户必须卸载现有的 （更高版本） 版本的组件，并重新安装已还原的 MSI 文件中的较旧版本。  
  
## <a name="software-servicing-topics"></a>软件维护主题  
以下主题介绍如何管理软件维护服务在设备上：  
  
-   [下载并应用 Microsoft 更新&#40;分析平台系统&#41;](download-and-apply-microsoft-updates.md)  
  
-   [卸载 Microsoft 更新&#40;分析平台系统&#41;](uninstall-microsoft-updates.md)  
  
-   [应用分析平台系统的修补程序&#40;分析平台系统&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [卸载分析平台系统修补程序&#40;分析平台系统&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
