---
title: 卸载 Microsoft 更新 (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df61570a-210d-4154-822f-98acd721f075
caps.latest.revision: 19
ms.openlocfilehash: b428cdacefefa96cdd5c500d34225c6963f5cb1f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="uninstall-microsoft-updates"></a>卸载 Microsoft 更新
本主题介绍如何卸载以前安装的 Microsoft 更新在分析平台系统设备上。  
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>必要條件  
若要执行这些步骤，你将需要：  
  
-   有权访问管理控制台监视设备分析平台系统登录名。  
  
-   Fabric 域管理员帐户登录到的知识 *<Fabric Domain>* * *-HST01** 节点。  
  
## <a name="HowToUninstallMSFT"></a>若要卸载 Microsoft 更新  
  
1.  登录到 *<Fabric Domain>* * *-HST01** 节点作为构造域管理员联系。  
  
2.  若要卸载所有的 WSUS，以卸载批准的更新，请打开命令提示符窗口并输入以下命令。 替换占位符项*/<*的相应信息。  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="see-also"></a>另请参阅  
[下载并应用 Microsoft 更新&#40;分析平台系统&#41;](download-and-apply-microsoft-updates.md)  
[将分析平台系统修补程序应用&#40;分析平台系统&#41;](apply-analytics-platform-system-hotfixes.md)  
[卸载分析平台系统修补程序&#40;分析平台系统&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[软件维护&#40;分析平台系统&#41;](software-servicing.md)  
  
