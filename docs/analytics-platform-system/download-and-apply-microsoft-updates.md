---
title: 下载 Microsoft 更新的分析平台系统 |Microsoft Docs
description: 本主题讨论如何为 Windows Server Update Services (WSUS) 从 Microsoft 更新目录下载更新并将这些更新应用于分析平台系统 appliance 服务器。 Microsoft Update 将 Windows 和 SQL Server 安装所有合适的更新。 VMM 虚拟机的设备上安装 WSUS。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d71a6ddc965b422f0f96f40788352213501b4db2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042295"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>下载和分析平台系统为应用 Microsoft 更新
本主题讨论如何为 Windows Server Update Services (WSUS) 从 Microsoft 更新目录下载更新并将这些更新应用于分析平台系统 appliance 服务器。 Microsoft Update 将 Windows 和 SQL Server 安装所有合适的更新。 VMM 虚拟机的设备上安装 WSUS。  
  
## <a name="TOP"></a>开始之前  
  
> [!WARNING]  
> 不尝试应用更新，如果你的设备或设备的任何组件向下或处于故障转移状态。 在这种情况下，与支持联系以获得帮助。  
>   
> 当设备正在使用时，不适用于 Microsoft 更新。 应用更新可能会导致设备节点重新启动。 未使用设备时，应在维护时段内应用更新。  
  
### <a name="prerequisites"></a>先决条件  
然后再执行这些步骤，您需要：  
  
-   按照中的说明在设备上配置 WSUS[配置 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)。  
  
-   Fabric 域管理员帐户登录信息的知识。  
  
-   具有登录名有权访问分析平台系统管理员控制台并查看设备状态信息。  
  
-   在大多数情况下，WSUS 需要访问设备外的服务器。 若要支持这种分析平台系统 DNS 可以配置为支持将允许使用外部 DNS 服务器解析名称分析平台系统主机和虚拟机 (Vm) 的外部名称转发器之外的使用方案设备。 有关详细信息，请参阅[使用 DNS 转发器解析非设备 DNS 名称&#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)。  
  
## <a name="bkmk_ImportUpdates"></a>若要下载并应用 Microsoft 更新  
  
#### <a name="verify-the-appliance-state-indicators"></a>验证设备状态指示器  
  
1.  打开管理控制台并导航到设备状态页。 有关详细信息，请参阅[通过使用管理控制台监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  验证设备状态上的所有节点的状态指示符。  
  
    -   它可以安全地继续绿色或 NA 指示器。  
  
    -   非关键 （黄色） 警告错误的计算结果。 在某些情况下警告消息不会阻止更新。 如果不在 C:\ 驱动器的非关键磁盘卷错误，就可以解决磁盘卷错误前继续执行下一步。  
  
    -   继续操作之前，必须解决大多数的红色指示器。 如果磁盘故障，请使用管理员控制台警报页以验证每个服务器或 SAN 阵列中的多个磁盘发生故障。 如果每个服务器或 SAN 阵列中的多个磁盘故障，你可以继续执行下一步之前修复磁盘故障。 请务必联系 Microsoft 支持部门以尽可能快地修复磁盘故障。  
  
#### <a name="synchronize-the-wsus-server"></a>将 WSUS 服务器同步  
  
1.  以域管理员身份登录到 VMM 虚拟机。  
  
2.  在中**服务器管理器仪表板**，然后在**工具**菜单中，单击**Windows Server Update Services** (**wsus.msc**)。  
  
3.  在 WSUS 管理控制台中，单击**同步**。  
  
4.  如果未运行同步，请单击**立即同步**右窗格中。 在底部窗格中，将同步状态。 等待，直到完成同步。  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>批准在 WSUS 中的 Microsoft 更新  
  
1.  在 WSUS 控制台中，左窗格中单击**的所有更新**。  
  
2.  在中**的所有更新**窗格中，单击**审批**下拉列表菜单中，将**审批**到**Any 除拒绝**。 单击**状态**下拉列表菜单中，将**状态**到**任何**。 单击 **“刷新”**。  
  
    右键单击**标题**列并选择**文件状态**在下载完成后验证文件状态。  
  
    您还可以选择**关键更新**或**安全更新**中这些类别的左窗格和视图可用更新。  
  
    ![选择所有更新并将状态更改为任何。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  选择所有更新，然后单击**批准**右窗格中的链接。  
  
    您可以右键单击所选的更新，然后单击**批准**。 您可能会提示接受"Microsoft 软件许可条款"。 如果是这样，请单击**我接受**中窗口以继续。  
  
    ![选择所有适用的更新并单击批准。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  选择设备服务器组中创建[配置 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)。  
  
5.  单击**批准安装**，然后单击**确定**。  
  
    ![批准您的计算机组的更新。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  在中**批准进度**对话框中，审批过程完成后，单击**关闭**。  
  
    ![批准更新时，请关闭窗口。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>验证更新在 WSUS 中  
  
-  验证所有更新的文件状态。 每个文件需要具有一个标题的左侧的绿色箭头图标。 这表明该文件已准备好进行安装。  
  
    ![文件状态为成功](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    之前安装的更新，请确保它们是所有已下载并在 WSUS 控制台中可用。  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>若要验证下载所有更新  
  
-  检查**下载状态**的更新在 WSUS 控制台中，如以下屏幕截图中所示。 检查**需文件更新**为 0，若要确认会下载所有更新。 如果此数字为大于零，可能需要返回并审批其他更新。  
  
    ![验证会下载所有更新。](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>应用 Microsoft 更新  
  
1.  在开始之前，打开[通过使用管理控制台监视设备&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)，单击**设备状态**选项卡，并确认**群集**并**网络**所有节点的列显示绿色 （或 NA）。 如果在两列中存在的任何警报，设备可能无法正确安装更新。 地址中的所有现有警报**群集**并**网络**继续操作之前的列。  
  
2.  登录到 _< 域名 >_**-HST01**节点作为 Fabric 域管理员。  
  
3.  若要将应用上为 WSUS 批准所有更新，运行更新程序。 请参阅[运行更新程序](#RunUpdateWizard)下面的说明。  
  
#### <a name="verify-the-updates-on-all-nodes"></a>验证所有节点上的更新  
  
1.  从 VMM 节点，启动 WSUS 管理控制台。 可在此应用程序下找到**启动**，**管理工具**， **Windows Server Update Services**。  
  
2.  展开**计算机**。  
  
3.  展开**的所有计算机**。  
  
4.  选择设备服务器组中创建[配置 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)。  
  
5.  在中**状态**下拉列表菜单中，选择**任何**然后单击**刷新**。  
  
6.  展开**更新服务**， *<appliance name>* VMM，**更新**，**的所有更新**，其中 *<appliance name>* 是您的设备名称。  
  
7.  在中**的所有更新**窗口中设置**审批**到**Any 除拒绝**。  
  
8.  在中**的所有更新**窗口中，将**状态**到**失败或需要**。  
  
9. 单击 **“刷新”**。  
  
10. 如果**所需的更新**大于零，支持人员联系以获得帮助。  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>请确保 SQL Server PDW 管理控制台中有无关键警报  
  
1.  打开管理控制台中，单击设备状态选项卡。请参阅[通过使用管理控制台监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-the-admin-console.md)。  
  
2.  确认**群集**并**网络**所有节点的列显示绿色 （或 NA）。 如果在两列中存在的任何警报，设备可能无法正确安装更新。 如果有任何严重警报，请联系支持。  
  
## <a name="RunUpdateWizard"></a>运行更新程序  
按照这些说明来运行分析平台系统更新程序。  
  
> [!NOTE]  
> WSUS 系统设计为运行以异步方式可能需要一些时间才能完全应用所有更新。 启动更新计划更新，但不会保证立即更新活动。  
  
1.  请确保您已登录到 HST01 节点作为 Fabric 域管理员。  
  
2.  打开命令提示符窗口并输入以下命令。 替换 *<parameter>* 与指定的信息。  
  
**若要运行 Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**若要报告 Microsoft 更新状态：**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>请参阅  
[卸载 Microsoft 更新&#40;分析平台系统&#41;](uninstall-microsoft-updates.md)  
[应用分析平台系统的修补程序&#40;分析平台系统&#41;](apply-analytics-platform-system-hotfixes.md)  
[卸载分析平台系统修补程序&#40;分析平台系统&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[软件维护服务&#40;分析平台系统&#41;](software-servicing.md)  
  
