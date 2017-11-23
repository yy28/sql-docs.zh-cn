---
title: "软件维护 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cec4d924-c88f-470c-84bb-0af3e21aabf1
caps.latest.revision: "33"
ms.openlocfilehash: 9741ca7440e8ec1dd0a40ff7e19a98ec6cc02cf2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="software-servicing"></a>软件维护
本部分总结了服务 Analytics Platform System 设备，包括 WSUS 和分析平台系统的修补程序的要求的软件。  
  
## <a name="Basics"></a>维护基础知识的软件  
**WSUS:**你分析平台系统的设备需要将配置为接收从 Windows Server Update Services (WSUS) 的更新。 这些更新包括对设备软件的重要更改。 它们进行配置后，许多更新都将自动安装，并不需要手动管理。 通常，将 WSUS 更新配置期间[配置 Windows Server Update Services &#40;WSUS &#41;&#40;分析平台系统 &#41;](configure-windows-server-update-services-wsus.md)新设备安装期间执行的步骤。 如果没有，可以稍后执行此配置步骤。 有关 WSUS 的信息，请参阅[WSUS 网站指南](http://go.microsoft.com/fwlink/?LinkId=202417)。  
  
**修补程序：**此外，你可能需要应用 Analytics Platform System 修补程序。 A*修补程序*是为特定客户来解决问题，分析平台系统软件创建的软件更新。 每个修补程序是安装特定于客户的问题的修补程序可执行文件。 每个修补程序还包含用于 Windows、 SQL Server 和分析平台系统的所有以前发布的软件更新的累积。 如果你需要安装修补程序，Microsoft 支持将为你提供的修补程序和说明。  
  
**作用域的更新：**将修补程序或服务包应用于分析平台系统必须使整个设备脱机。 也就是说，不会影响 PDW 和 HDInsight 区域。  
  
**SSIS 目标适配器和客户端工具：**应用修补程序时，包括对 SSIS 目标适配器 MSI 的更改或 MSI 文件将更新在客户端工具 MSI **C:\PDWINST\ClientTools**在管理节点上的目录。 修补程序不会自动安装组件从更新的 MSI 文件。 若要更新这些组件，客户必须卸载旧版本的组件，并从更新的 MSI 文件安装新版本。 在卸载修补程序时，包括对 SSIS 目标适配器 MSI 的更改，或客户端工具 MSI，这些组件的 MSI 文件将还原到以前的版本。 若要还原到以前的版本的这些组件，客户必须先卸载现有的 （较新） 版本的组件，并重新安装恢复后的 MSI 文件中的较旧版本。  
  
## <a name="software-servicing-topics"></a>软件维护主题  
以下主题介绍如何管理软件维护服务在设备上：  
  
-   [下载并应用 Microsoft 更新 &#40;分析平台系统 &#41;](download-and-apply-microsoft-updates.md)  
  
-   [卸载 Microsoft 更新 &#40;分析平台系统 &#41;](uninstall-microsoft-updates.md)  
  
-   [应用分析平台系统修补程序 &#40;分析平台系统 &#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [卸载分析平台系统修补程序 &#40;分析平台系统 &#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
