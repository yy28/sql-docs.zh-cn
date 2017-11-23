---
title: "卸载分析平台系统修补程序 (Analytics Platform System)"
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
ms.assetid: c9ab596d-3f5a-48e2-bce7-c9be99b8c23b
caps.latest.revision: "21"
ms.openlocfilehash: 04740eeccc1b7837c278ce0041cc1e6f78fd4c60
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>卸载分析平台系统修补程序
以下步骤介绍如何卸载以前安装的分析平台系统修补程序。  
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>先决条件  
若要执行这些步骤，你将需要：  
  
-   有权访问管理控制台监视设备分析平台系统登录。  
  
-   域管理员帐户登录到*< appliance_domain >***-HST01**节点。  
  
-   知识库文章编号，为了使修补程序以卸载。  
  
## <a name="HowToUninstallPDW"></a>若要卸载 SQL Server PDW 修补程序  
  
1.  登录到*< appliance_domain >***-HST01**节点作为构造域管理员联系。  
  
2.  使用作为管理员选项运行以打开命令提示符。  
  
3.  将目录更改为`C:\PDWINST\Patches\<kbarticle>\media`其中 *<kbarticle>* 是为了使修补程序的知识库文章编号，以卸载。  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  若要移除此修补程序，请运行以下命令。  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>另请参阅  
[下载并应用 Microsoft 更新 &#40;分析平台系统 &#41;](download-and-apply-microsoft-updates.md)  
[卸载 Microsoft 更新 &#40;分析平台系统 &#41;](uninstall-microsoft-updates.md)  
[应用分析平台系统修补程序 &#40;分析平台系统 &#41;](apply-analytics-platform-system-hotfixes.md)  
[软件维护 &#40;分析平台系统 &#41;](software-servicing.md)  
  
