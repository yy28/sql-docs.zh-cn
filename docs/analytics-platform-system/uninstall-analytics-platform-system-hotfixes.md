---
title: 卸载 Analytics Platform System 修补程序在 |Microsoft Docs
description: 卸载 Analytics Platform System 修补程序。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5507eae7bb2f8a5ce138223a031ac4946d9f0030
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255063"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>卸载 Analytics Platform System 修补程序 
以下步骤介绍如何卸载以前安装的 Analytics Platform System 修补程序。  
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>先决条件  
若要执行这些步骤，将需要：  
  
-   有权访问管理控制台来监视设备分析平台系统登录名。  
  
-   域管理员帐户登录到<em>< appliance_domain ></em>**-HST01**节点。  
  
-   知识库文章编号，为了使修补程序以卸载。  
  
## <a name="HowToUninstallPDW"></a>若要卸载 SQL Server PDW 修补程序  
  
1.  登录到<em>< appliance_domain ></em>**-HST01**节点作为 Fabric 域管理员。  
  
2.  使用运行方式管理员选项打开命令提示符。  
  
3.  将目录更改为`C:\PDWINST\Patches\<kbarticle>\media`其中*<kbarticle>* 是为了使修补程序的知识库文章编号，以卸载。  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  若要删除该修补程序，请运行以下命令。  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>请参阅  
[下载并应用 Microsoft 更新&#40;分析平台系统&#41;](download-and-apply-microsoft-updates.md)  
[卸载 Microsoft 更新&#40;分析平台系统&#41;](uninstall-microsoft-updates.md)  
[应用分析平台系统的修补程序&#40;分析平台系统&#41;](apply-analytics-platform-system-hotfixes.md)  
[软件维护服务&#40;分析平台系统&#41;](software-servicing.md)  
  
