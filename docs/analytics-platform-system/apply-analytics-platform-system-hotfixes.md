---
title: 应用 Analytics Platform System 修补程序
description: 本文介绍如何向分析平台系统软件应用修补程序。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd62413ec8542aba9f3973d0e8483cb9c5c9128a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401373"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>应用 Analytics Platform System 修补程序
本文介绍如何向分析平台系统软件应用修补程序。  
  
## <a name="before-you-begin"></a>开始之前  
  
> [!WARNING]  
> 如果设备或任何设备组件关闭或处于故障转移状态，请不要尝试应用分析平台系统修补程序。 在这种情况下，请联系支持人员获取帮助。  
  
> [!WARNING]  
> 请勿在设备使用时应用分析平台系统修补程序。 应用修补程序可能会导致设备节点重新启动。 如果未使用设备，则应在维护时段内应用此修补程序。  
  
### <a name="prerequisites"></a>先决条件  
若要执行这些步骤，你将需要：  
  
-   一个分析平台系统登录，有权访问管理控制台来监视设备状态。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   了解用于连接到 _<domain_name>_**节点的**Fabric 域管理员帐户。  
  
## <a name="to-apply-a-analytics-platform-system-hotfix"></a><a name="HowToInstallPDW"></a>应用分析平台系统修补程序  
与 Microsoft 更新不同，分析平台系统软件的修补程序不会通过 WSUS 进行处理。 它们具有不同的工作流，并通过运行修补程序包来安装。  
  
1.  **验证设备状态指示器。**  
  
    1.  打开管理控制台并导航到 "设备状态" 页。 有关详细信息，请参阅[使用管理控制台监视设备 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  在继续下一步之前，必须解决所有红色或黄色指示器。 下面是一些例外情况：  
  
        -   如果出现磁盘故障，请使用管理控制台的 "警报" 页来验证每个服务器或 SAN 阵列内是否不存在多个磁盘故障。 如果每个服务器或 SAN 阵列中不存在多个磁盘故障，则可以在修复磁盘故障之前继续下一步。 请确保联系 Microsoft 支持部门尽快修复磁盘故障。  
  
        -   如果非关键（黄色）磁盘卷错误不在 C：\ 上驱动器，你可以在解决磁盘卷错误之前执行下一步。  
  
2.  **安装分析平台系统修补程序**  
  
    1.  以域管理员身份登录到 <*appliance_domain*>-HST01 节点。  
  
    2.  使用 "以**管理员身份运行**" 选项打开命令提示符。  
  
    3.  运行以下命令，将替换*<HotfixPackageName>* 为修补程序可执行文件包的名称，并将 *<  >* 的其他占位符项替换为相应的信息。  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  按照修补程序包中的步骤进行操作。  
  
## <a name="see-also"></a>另请参阅  
[&#40;Analytics Platform System&#41;下载并应用 Microsoft 更新](download-and-apply-microsoft-updates.md)  
[&#40;Analytics Platform System&#41;卸载 Microsoft 更新](uninstall-microsoft-updates.md)  
[&#40;Analytics Platform System&#41;卸载分析平台系统修补程序](uninstall-analytics-platform-system-hotfixes.md)  
[软件服务 &#40;分析平台系统&#41;](software-servicing.md)  
  
