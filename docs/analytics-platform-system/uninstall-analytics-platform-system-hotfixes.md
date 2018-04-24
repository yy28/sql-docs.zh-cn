---
title: 卸载分析平台系统中的修补程序 |Microsoft 文档
description: 卸载 Analytics Platform System 修补程序。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 83e57a676ee0eff21eb3a736484d8e286cdeee01
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>卸载 Analytics Platform System 修补程序 
以下步骤介绍如何卸载以前安装的分析平台系统修补程序。  
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>必要條件  
若要执行这些步骤，你将需要：  
  
-   有权访问管理控制台监视设备分析平台系统登录。  
  
-   域管理员帐户登录到*< appliance_domain > * * *-HST01** 节点。  
  
-   知识库文章编号，为了使修补程序以卸载。  
  
## <a name="HowToUninstallPDW"></a>若要卸载 SQL Server PDW 修补程序  
  
1.  登录到*< appliance_domain > * * *-HST01** 节点作为构造域管理员联系。  
  
2.  使用作为管理员选项运行以打开命令提示符。  
  
3.  将目录更改为`C:\PDWINST\Patches\<kbarticle>\media`其中*<kbarticle>*是为了使修补程序的知识库文章编号，以卸载。  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  若要移除此修补程序，请运行以下命令。  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>另请参阅  
[下载并应用 Microsoft 更新&#40;分析平台系统&#41;](download-and-apply-microsoft-updates.md)  
[卸载 Microsoft 更新&#40;分析平台系统&#41;](uninstall-microsoft-updates.md)  
[将分析平台系统修补程序应用&#40;分析平台系统&#41;](apply-analytics-platform-system-hotfixes.md)  
[软件维护&#40;分析平台系统&#41;](software-servicing.md)  
  
