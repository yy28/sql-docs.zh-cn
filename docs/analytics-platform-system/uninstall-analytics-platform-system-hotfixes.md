---
title: 卸载分析平台系统修补程序 (Analytics Platform System)
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
ms.assetid: c9ab596d-3f5a-48e2-bce7-c9be99b8c23b
caps.latest.revision: 21
ms.openlocfilehash: 56c6731d5a39741574999d94532b9505adaf6380
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>卸载分析平台系统修补程序
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
  
