---
title: 卸载 Microsoft 更新
description: 卸载分析平台系统（AP）中的 Microsoft 更新。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a5ebe1ee911f7500505cdbd1962d28c35461a635
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399458"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>卸载分析平台系统中的 Microsoft 更新
本文介绍如何在 Analytics Platform System 设备上卸载以前安装的 Microsoft 更新。  
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>先决条件  
若要执行这些步骤，你将需要：  
  
-   一个分析平台系统登录，有权访问管理控制台来监视设备。  
  
-   了解用于<em> <Fabric Domain> </em>登录到 **-HST01**节点的 Fabric 域管理员帐户。  
  
## <a name="to-uninstall-microsoft-updates"></a><a name="HowToUninstallMSFT"></a>卸载 Microsoft 更新  
  
1.  以 Fabric 域管理员<em> <Fabric Domain> </em>身份登录到 **-HST01**节点。  
  
2.  若要卸载已批准 WSUS 卸载的所有更新，请打开命令提示符窗口并输入以下命令。 将 *<  >* 的占位符项替换为相应的信息。  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>后续步骤
有关详细信息，请参见:
- [&#40;Analytics Platform System&#41;下载并应用 Microsoft 更新](download-and-apply-microsoft-updates.md) 
- [&#40;Analytics Platform System&#41;应用分析平台系统修补程序](apply-analytics-platform-system-hotfixes.md)  
- [&#40;Analytics Platform System&#41;卸载分析平台系统修补程序](uninstall-analytics-platform-system-hotfixes.md)  
- [软件服务 &#40;分析平台系统&#41;](software-servicing.md)  
  
