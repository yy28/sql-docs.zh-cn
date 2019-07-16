---
title: 卸载 Microsoft 更新的分析平台系统 |Microsoft Docs"
description: 卸载 Microsoft 更新中 Analytics Platform System (APS)。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f910eeb7f3b38d29f7ae7b084de981c22a6f3f4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959834"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>卸载 Microsoft 分析平台系统中的更新
本文介绍如何卸载以前安装的 Microsoft 更新在分析平台系统设备上。  
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>先决条件  
若要执行这些步骤，将需要：  
  
-   有权访问管理控制台来监视设备分析平台系统登录名。  
  
-   Fabric 域管理员帐户登录到的知识<em> <Fabric Domain> </em> **-HST01**节点。  
  
## <a name="HowToUninstallMSFT"></a>若要卸载 Microsoft 更新  
  
1.  登录到<em> <Fabric Domain> </em> **-HST01**节点作为 Fabric 域管理员。  
  
2.  若要卸载的 WSUS，以卸载批准的所有更新，请打开命令提示符窗口并输入以下命令。 替换占位符项 *< >* 的相应信息。  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>后续步骤
有关详细信息，请参阅：
- [下载并应用 Microsoft 更新&#40;分析平台系统&#41;](download-and-apply-microsoft-updates.md) 
- [应用分析平台系统的修补程序&#40;分析平台系统&#41;](apply-analytics-platform-system-hotfixes.md)  
- [卸载分析平台系统修补程序&#40;分析平台系统&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [软件维护服务&#40;分析平台系统&#41;](software-servicing.md)  
  
