---
title: 卸载 Microsoft 更新-分析平台系统 |Microsoft 文档"
description: 卸载 Microsoft 更新中分析平台系统 (AP)。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 57d0eb3616cf3567f63d75029f79cea6709ed955
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538547"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>卸载分析平台系统中的 Microsoft 更新
本文介绍如何卸载以前安装的 Microsoft 更新在分析平台系统设备上。  
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>必要條件  
若要执行这些步骤，你将需要：  
  
-   有权访问管理控制台监视设备分析平台系统登录。  
  
-   Fabric 域管理员帐户登录到的知识 *<Fabric Domain>* * *-HST01** 节点。  
  
## <a name="HowToUninstallMSFT"></a>若要卸载 Microsoft 更新  
  
1.  登录到 *<Fabric Domain>* * *-HST01** 节点作为构造域管理员联系。  
  
2.  若要卸载所有的 WSUS，以卸载批准的更新，请打开命令提示符窗口并输入以下命令。 替换占位符项 */<* 的相应信息。  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>后续步骤
有关详细信息，请参阅：
- [下载并应用 Microsoft 更新&#40;分析平台系统&#41;](download-and-apply-microsoft-updates.md) 
- [将分析平台系统修补程序应用&#40;分析平台系统&#41;](apply-analytics-platform-system-hotfixes.md)  
- [卸载分析平台系统修补程序&#40;分析平台系统&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [软件维护&#40;分析平台系统&#41;](software-servicing.md)  
  
