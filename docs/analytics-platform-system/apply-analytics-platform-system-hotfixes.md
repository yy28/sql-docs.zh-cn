---
title: 应用分析平台系统修补程序 (Analytics Platform System)
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
ms.assetid: fca5eec9-86b8-4d20-b498-1678c367b5c8
caps.latest.revision: 25
ms.openlocfilehash: 1a054ead9ef39169257eb1813ba49eae06082b96
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="apply-analytics-platform-system-hotfixes"></a>应用分析平台系统修补程序
本主题讨论如何将修补程序应用于分析平台系统软件。  
  
## <a name="before-you-begin"></a>开始之前  
  
> [!WARNING]  
> 请不要尝试应用 Analytics Platform System 修补程序，如果你的设备或设备的任何组件是向下或处于故障转移状态。 在这种情况下，请联系支持部门以获取帮助。  
  
> [!WARNING]  
> 当设备正在使用时，不适用于分析平台系统修补程序。 应用修补程序可能会导致设备节点重新启动。 当不使用该设备时，应在维护时段内应用此修补程序。  
  
### <a name="prerequisites"></a>必要條件  
若要执行这些步骤，你将需要：  
  
-   有权访问管理控制台来监视的设备状态分析平台系统登录。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   要连接到的结构域管理员帐户的知识*< 域名 > * * *-HST01** 节点。  
  
## <a name="HowToInstallPDW"></a>要应用 Analytics Platform System 修补程序  
与 Microsoft 更新中，不同的分析平台系统软件修补程序不处理通过 WSUS 中。 它们具有不同的工作流和通过运行修补程序包安装。  
  
1.  **验证设备状态指示器。**  
  
    1.  打开管理控制台并导航到的设备状态页。 有关详细信息，请参阅[通过使用管理控制台监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  必须先解决所有的红色或黄色指示器，然后继续下一步。 是几个例外：  
  
        -   如果有磁盘故障，使用管理员控制台警报页面以验证没有中每个服务器或 SAN 阵列的多个磁盘故障。 如果没有在每个服务器或 SAN 阵列的多个磁盘故障，就可以在修复磁盘失败之前继续执行下一步。 请务必请联系 Microsoft 支持，以尽可能快地解决磁盘失败。  
  
        -   如果没有非关键 （黄色） 的磁盘卷错误将不在 C:\ 驱动器上，你可以继续执行下一步之前解决磁盘卷错误。  
  
2.  **安装 Analytics Platform System 修补程序**  
  
    1.  登录到 <*appliance_domain*>-HST01 节点以域管理员。  
  
    2.  使用**以管理员身份运行**选项来打开命令提示符。  
  
    3.  运行以下命令，替换*<HotfixPackageName>*同名的修补程序可执行文件包，并将其他占位符项*/<*的相应信息。  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  提供的修补程序包，请执行的步骤。  
  
## <a name="see-also"></a>另请参阅  
[下载并应用 Microsoft 更新&#40;分析平台系统&#41;](download-and-apply-microsoft-updates.md)  
[卸载 Microsoft 更新&#40;分析平台系统&#41;](uninstall-microsoft-updates.md)  
[卸载分析平台系统修补程序&#40;分析平台系统&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[软件维护&#40;分析平台系统&#41;](software-servicing.md)  
  
