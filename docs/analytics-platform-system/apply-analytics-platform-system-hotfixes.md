---
title: 应用 Analytics Platform System 修补程序 |Microsoft Docs
description: 本文介绍如何将修补程序应用于分析平台系统软件。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b4b72017bb23ae44da9c5884f0ebf2a8b099fd3e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63019042"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>应用 Analytics Platform System 修补程序
本文介绍如何将修补程序应用于分析平台系统软件。  
  
## <a name="before-you-begin"></a>开始之前  
  
> [!WARNING]  
> 不尝试应用 Analytics Platform System 修补程序，如果你的设备或设备的任何组件向下或处于故障转移状态。 在这种情况下，与支持联系以获得帮助。  
  
> [!WARNING]  
> 设备正在使用中，则不应用 Analytics Platform System 修补程序。 应用修补程序可能会导致设备节点重新启动。 当不使用该设备时，应在维护时段内应用此修补程序。  
  
### <a name="prerequisites"></a>先决条件  
若要执行这些步骤，将需要：  
  
-   有权访问管理控制台监视设备状态分析平台系统登录名。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Fabric 域管理员帐户连接到的知识 _< 域名 >_**-HST01**节点。  
  
## <a name="HowToInstallPDW"></a>若要应用 Analytics Platform System 修补程序  
与 Microsoft 更新中，不同的分析平台系统软件修补程序不通过 WSUS 处理。 在具有不同的工作流，并通过运行修补程序包安装。  
  
1.  **验证设备状态指示器。**  
  
    1.  打开管理控制台并导航到设备状态页。 有关详细信息，请参阅[通过使用管理控制台监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  在继续进行下一步之前，必须解析所有红色或黄色指示器。 几个例外情况是：  
  
        -   如果磁盘故障，请使用管理员控制台警报页以验证每个服务器或 SAN 阵列中的多个磁盘发生故障。 如果每个服务器或 SAN 阵列中的多个磁盘故障，你可以继续执行下一步之前修复磁盘故障。 请务必联系 Microsoft 支持部门以尽可能快地修复磁盘故障。  
  
        -   如果不在 C:\ 驱动器的非关键 （黄色） 磁盘卷错误，就可以解决磁盘卷错误前继续执行下一步。  
  
2.  **安装 Analytics Platform System 修补程序**  
  
    1.  登录到 <*appliance_domain*>-HST01 节点以域管理员。  
  
    2.  使用**以管理员身份运行**选项来打开命令提示符。  
  
    3.  运行以下命令，替换 *<HotfixPackageName>* 修补程序可执行文件包，并替换占位符中的其他项的名称 *< >* 的相应信息。  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  主讲人修补程序包，请执行的步骤。  
  
## <a name="see-also"></a>请参阅  
[下载并应用 Microsoft 更新&#40;分析平台系统&#41;](download-and-apply-microsoft-updates.md)  
[卸载 Microsoft 更新&#40;分析平台系统&#41;](uninstall-microsoft-updates.md)  
[卸载分析平台系统修补程序&#40;分析平台系统&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[软件维护服务&#40;分析平台系统&#41;](software-servicing.md)  
  
