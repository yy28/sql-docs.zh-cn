---
title: 卸载修补程序
description: 卸载分析平台系统修补程序。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef6929aeb06c9472eb3ff210de016117a9636ded
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399767"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>卸载分析平台系统修补程序 
以下步骤介绍如何卸载以前安装的分析平台系统修补程序。  
  
## <a name="before-you-begin"></a>开始之前  
  
### <a name="prerequisites"></a>先决条件  
若要执行这些步骤，你将需要：  
  
-   一个分析平台系统登录，有权访问管理控制台来监视设备。  
  
-   用于登录到<em><appliance_domain></em> **-HST01**节点的域管理员帐户。  
  
-   要卸载的修补程序的知识库文章编号。  
  
## <a name="to-uninstall-a-sql-server-pdw-hotfix"></a><a name="HowToUninstallPDW"></a>卸载 SQL Server PDW 修补程序  
  
1.  以 Fabric 域管理员身份登录到<em><appliance_domain></em> **-HST01**节点。  
  
2.  使用 "以管理员身份运行" 选项打开命令提示符。  
  
3.  将目录更改为 `C:\PDWINST\Patches\<kbarticle>\media` ，其中 *<kbarticle>* 是要卸载的修补程序的知识库文章编号。  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  若要删除此修补程序，请运行以下命令。  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>另请参阅  
[&#40;Analytics Platform System&#41;下载并应用 Microsoft 更新 ](download-and-apply-microsoft-updates.md)  
[&#40;Analytics Platform System&#41;卸载 Microsoft 更新 ](uninstall-microsoft-updates.md)  
[&#40;Analytics Platform System&#41;应用分析平台系统修补程序 ](apply-analytics-platform-system-hotfixes.md)  
[软件服务 &#40;分析平台系统&#41;](software-servicing.md)  
  
