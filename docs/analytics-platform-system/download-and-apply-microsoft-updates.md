---
title: 下载 Analytics Platform System 的 Microsoft 更新-|Microsoft 文档
description: 本主题讨论如何从 Microsoft 更新目录到 Windows Server Update Services (WSUS) 下载更新并将这些更新应用于分析平台系统设备服务器。 Microsoft 更新将安装所有合适的更新，Windows 和 SQL Server。 VMM 虚拟机的设备上安装 WSUS。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b98a2be90f222fc2c531c1f1983f8882bdab640e
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>下载并针对分析平台系统中应用 Microsoft 更新
本主题讨论如何从 Microsoft 更新目录到 Windows Server Update Services (WSUS) 下载更新并将这些更新应用于分析平台系统设备服务器。 Microsoft 更新将安装所有合适的更新，Windows 和 SQL Server。 VMM 虚拟机的设备上安装 WSUS。  
  
## <a name="TOP"></a>开始之前  
  
> [!WARNING]  
> 请不要尝试应用更新，如果你的设备或设备的任何组件是向下或处于故障转移状态。 在这种情况下，请联系支持部门以获取帮助。  
>   
> 当设备正在使用时，不适用于 Microsoft 更新。 应用更新可能会导致设备节点重新启动。 当不使用该设备时，应在维护时段内应用这些更新。  
  
### <a name="prerequisites"></a>必要條件  
在执行这些步骤之前, 你需要：  
  
-   中的说明在你的设备上配置 WSUS[配置 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)。  
  
-   结构域管理员帐户登录信息的知识。  
  
-   有一个登录名有权访问分析平台系统管理员控制台并查看设备状态信息。  
  
-   在大多数情况下，WSUS 需要访问外部设备的服务器。 若要支持这种分析平台系统 DNS 可以配置为支持将允许使用外部 DNS 服务器来解析名称 Analytics Platform System 主机和虚拟机 (Vm) 的外部名称转发器之外的使用方案设备。 有关详细信息，请参阅[使用 DNS 转发器来解决非设备 DNS 名称&#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)。  
  
## <a name="bkmk_ImportUpdates"></a>若要下载并应用 Microsoft 更新  
  
#### <a name="verify-the-appliance-state-indicators"></a>验证设备状态指示器  
  
1.  打开管理控制台并导航到的设备状态页。 有关详细信息，请参阅[通过使用管理控制台监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  验证设备状态的所有节点的状态指示符。  
  
    -   则可以安全地继续绿色或 NA 指示器。  
  
    -   评估 （黄色） 的非严重警告错误。 在某些情况下警告消息不会阻止更新。 如果没有非关键磁盘卷错误将不在 C:\ 驱动器上，你可以继续执行下一步之前解决磁盘卷错误。  
  
    -   在继续之前，必须解决大多数的红色指示器。 如果有磁盘故障，使用管理员控制台警报页面以验证没有中每个服务器或 SAN 阵列的多个磁盘故障。 如果没有在每个服务器或 SAN 阵列的多个磁盘故障，你可以继续执行下一步之前修复磁盘故障。 请务必请联系 Microsoft 支持，以尽可能快地解决磁盘故障。  
  
#### <a name="synchronize-the-wsus-server"></a>将 WSUS 服务器同步  
  
1.  以域管理员身份登录到 VMM 虚拟机。  
  
2.  在**服务器管理器仪表板**上**工具**菜单上，单击**Windows Server Update Services** (**wsus.msc**)。  
  
3.  在 WSUS 管理控制台中，单击**同步**。  
  
4.  如果同步未运行，请单击**立即同步**右窗格中。 在底部窗格中，将同步状态。 等待，直到完成同步。  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>批准 WSUS 中的 Microsoft 更新  
  
1.  在左窗格中，WSUS 控制台中，单击**所有更新**。  
  
2.  在**所有更新**窗格中，单击**批准**下拉菜单中，将**批准**到**Any 除拒绝**。 单击**状态**下拉菜单中，将**状态**到**任何**。 单击 **“刷新”**。  
  
    右键单击**标题**列并选择**文件状态**在下载完成后验证文件状态。  
  
    你还可以选择**关键更新**或**安全更新**在这些类别的左窗格中并查看可用更新。  
  
    ![选择所有更新，并将状态更改为任何。] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  选择所有更新，然后单击**批准**右窗格中的链接。  
  
    你可以右键单击所选的更新，，然后单击**批准**。 系统可能会提示你接受"Microsoft 软件许可条款"。 如果是这样，则单击**我接受**继续窗口中。  
  
    ![选择应用，并单击批准的所有更新。] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  选择你在中创建的设备服务器组[配置 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)。  
  
5.  单击**批准安装**，然后单击**确定**。  
  
    ![批准更新为你的计算机组。] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  在**批准进度**对话框中，审批过程完成后，单击**关闭**。  
  
    ![当批准更新后，请关闭窗口。] (./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>验证 WSUS 中有更新  
  
-  验证所有更新的文件状态。 每个文件需要具有标题左侧的绿色箭头图标。 这表明该文件已准备好进行安装。  
  
    ![文件状态为成功](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    在安装之前的更新，请确保它们是所有已下载并在 WSUS 控制台中可用。  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>若要验证下载的所有更新  
  
-  检查**下载状态**的更新在 WSUS 控制台中，如下面的屏幕截图中所示。 检查**无文件的更新**为 0，以确认下载所有更新。 如果此数字为大于零，可能需要返回并批准其他更新。  
  
    ![验证下载的所有更新。] (./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>应用 Microsoft 更新  
  
1.  在开始之前，打开[通过使用管理控制台监视设备&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)，单击**装置状态更改为**选项卡上，并确认**群集**和**网络**所有节点的列显示绿色 （或 NA）。 如果在任一这些列中存在任何警报，设备可能无法正确安装更新。 地址中的所有现有警报**群集**和**网络**列然后再继续。  
  
2.  登录到 *< 域名 > * * *-HST01** 节点作为构造域管理员联系。  
  
3.  若要将应用所有 wsus 批准的更新，运行更新程序。 请参阅[运行更新程序](#RunUpdateWizard)下面有关的说明。  
  
#### <a name="verify-the-updates-on-all-nodes"></a>验证所有节点上的更新  
  
1.  从 VMM 节点中，启动 WSUS 管理控制台。 此应用程序可以下找到**启动**，**管理工具**， **Windows Server Update Services**。  
  
2.  展开**计算机**。  
  
3.  展开**所有计算机**。  
  
4.  选择你在中创建的设备服务器组[配置 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)。  
  
5.  在**状态**下拉列表菜单上，选择**任何**单击**刷新**。  
  
6.  展开**更新服务**， *<appliance name>* VMM，**更新**，**所有更新**，其中 *<appliance name>* 是你的设备名称。  
  
7.  在**所有更新**窗口集**批准**到**Any 除拒绝**。  
  
8.  在**所有更新**窗口中，设置**状态**到**失败或需要**。  
  
9. 单击 **“刷新”**。  
  
10. 如果**所需的更新**大于零个、 支持联系以获取帮助。  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>确保在 SQL Server PDW 管理控制台中没有关键警报  
  
1.  打开管理控制台中，单击设备状态选项卡。请参阅[通过使用管理控制台监视设备&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。  
  
2.  验证**群集**和**网络**所有节点的列显示绿色 （或 NA）。 如果在任一这些列中存在任何警报，设备可能无法正确安装更新。 如果有任何严重警报，请联系支持部门。  
  
## <a name="RunUpdateWizard"></a>运行更新程序  
按照这些说明来运行分析平台系统更新程序。  
  
> [!NOTE]  
> WSUS 系统旨在为运行以异步方式可能需要一些时间才能完全应用所有更新。 启动更新计划更新，但不保证立即更新活动。  
  
1.  请确保你登录到 HST01 节点作为构造域管理员联系。  
  
2.  打开命令提示符窗口并输入以下命令。 替换*<parameter>* 与指定的信息。  
  
**若要运行 Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**若要报告的 Microsoft 更新状态：**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>另请参阅  
[卸载 Microsoft 更新&#40;分析平台系统&#41;](uninstall-microsoft-updates.md)  
[将分析平台系统修补程序应用&#40;分析平台系统&#41;](apply-analytics-platform-system-hotfixes.md)  
[卸载分析平台系统修补程序&#40;分析平台系统&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[软件维护&#40;分析平台系统&#41;](software-servicing.md)  
  
