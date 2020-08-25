---
title: 软件维护服务
description: 分析平台系统中的软件服务 (AP) 。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4325dfa9c16edba12c2bba694b47c1b0875c7c6f
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400317"
---
# <a name="software-servicing-in-analytics-platform-system"></a>分析平台系统中的软件服务
本部分汇总了针对分析平台系统设备（包括 WSUS 和分析平台系统修补程序）的软件服务要求。  
  
## <a name="software-servicing-basics"></a><a name="Basics"></a>软件维护基础知识  
**WSUS：** 需要将分析平台系统设备配置为接收来自 Windows Server Update Services (WSUS) 的更新。 这些更新包括对设备软件的重要更改。 配置完成后，许多更新会自动安装，不需要进行动手管理。 通常，WSUS 更新在 [配置 Windows Server Update Services &#40;wsus&#41; &#40;分析平台系统 ](configure-windows-server-update-services-wsus.md) 在安装新设备期间执行&#41;步骤的过程中进行配置。 如果不是，则可以在以后执行此配置步骤。 有关 WSUS 的信息，请参阅 [wsus 网站指南](https://go.microsoft.com/fwlink/?LinkId=202417)。  
  
**修补程序：** 此外，可能还需要应用分析平台系统修补程序。 *修补程序*是为特定客户创建的软件更新，用来解决分析平台系统软件的问题。 每个修补程序都是可执行文件，用于安装客户特定问题的修补程序。 每个修补程序还包含以前发布的适用于 Windows、SQL Server 和分析平台系统的所有软件更新。 如果需要安装修补程序，Microsoft 支持人员将为你提供修补程序和说明。  
  
**更新的范围：** 将修补程序或 Service Pack 应用到分析平台系统必须使整个设备脱机。  
  
**SSIS 目标适配器和客户端工具：** 应用包含对 SSIS 目标适配器 MSI 或客户端工具 MSI 的更改的修补程序时，会在控制节点上的 **C:\PDWINST\ClientTools** 目录中更新 MSI 文件。 此修补程序不会自动安装更新后的 MSI 文件中的组件。 若要更新这些组件，客户必须卸载旧版本的组件，并从更新的 MSI 文件中安装新版本。 卸载包含对 SSIS 目标适配器 MSI 或客户端工具 MSI 的更改的修补程序时，这些组件的 MSI 文件将还原为以前的版本。 若要将这些组件恢复到以前的版本，客户必须卸载现有 (新的) 版本的组件，然后从恢复的 MSI 文件重新安装旧版本。  
  
## <a name="software-servicing-topics"></a>软件维护主题  
以下主题介绍如何在设备上管理软件服务：  
  
-   [&#40;Analytics Platform System&#41;下载并应用 Microsoft 更新 ](download-and-apply-microsoft-updates.md)  
  
-   [&#40;Analytics Platform System&#41;卸载 Microsoft 更新 ](uninstall-microsoft-updates.md)  
  
-   [&#40;Analytics Platform System&#41;应用分析平台系统修补程序 ](apply-analytics-platform-system-hotfixes.md)  
  
-   [&#40;Analytics Platform System&#41;卸载分析平台系统修补程序 ](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
