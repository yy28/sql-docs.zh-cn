---
title: 配置 Windows Server Update Services (WSUS) (Analytics Platform System)
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
ms.assetid: a10b2884-468e-41ef-bd59-8df894381254
caps.latest.revision: 41
ms.openlocfilehash: 31427bc55017cf9c069e8cd4a467dfdb9608ca3f
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
---
# <a name="configure-windows-server-update-services-wsus"></a>配置 Windows Server Update Services (WSUS)
这些说明将引导你完成使用 Windows Server Update Services (WSUS) 配置向导配置 WSUS 以分析平台系统的步骤。 你需要先将软件更新应用到该设备配置 WSUS。 VMM 虚拟机的设备上已安装 WSUS。  
  
有关将 WSUS 配置的详细信息，请参阅[WSUS 分步安装指南](http://go.microsoft.com/fwlink/?LinkId=202417)WSUS 网站上。 后配置 WSUS，请参阅[下载和应用 Microsoft 更新&#40;Analytics Platform System&#41; ](download-and-apply-microsoft-updates.md)以启动更新。  
  
> [!WARNING]  
> 如果在此配置过程中遇到任何错误，停止，并与支持人员联系以获取帮助。 不要忽略错误或接收错误后继续在进程中。  
  
## <a name="before-you-begin"></a>开始之前  
若要配置 WSUS，你需要：  
  
-   具有 Analytics Platform System 设备域管理员帐户的登录信息。  
  
-   具有分析平台系统登录名有权访问**管理控制台**并查看设备状态信息。  
  
-   知道上游 WSUS 服务器的 IP 地址，如果你打算从上游 WSUS 服务器而不是同步更新直接从 Microsoft 更新同步更新。 请确保你上游 WSUS 服务器设置为允许匿名连接，并支持 SSL。  
  
-   知道代理服务器的 IP 地址，如果你的设备将使用代理服务器访问的上游服务器或 Microsoft 更新。  
  
-   在大多数情况下，WSUS 需要访问外部设备的服务器。 若要支持这种分析平台系统 DNS 可以配置为支持将允许使用外部 DNS 服务器来解析名称 Analytics Platform System 主机和虚拟机 (Vm) 的外部名称转发器之外的使用方案设备。 有关详细信息，请参阅[使用 DNS 转发器来解决非设备 DNS 名称&#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)。  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>若要配置 Windows Server Update Services (WSUS)  
  
1.  登录到**管理控制台**。 上**装置状态更改为**选项卡上，确认**群集**和**网络**列显示绿色 (或**NA**) 的所有节点。 在验证所有节点的状态指示符**装置状态更改为**。  
  
    -   则可以安全地继续绿色或 NA 指示器。  
  
    -   评估 （黄色） 的非严重警告错误。 在某些情况下警告消息不会阻止更新。 如果没有非关键磁盘卷错误将不在 C:\ 驱动器上，你可以继续执行下一步之前解决磁盘卷错误。  
  
    -   在继续之前，必须解决大多数的红色指示器。 如果磁盘故障，请使用**管理员控制台警报**页以验证是否没有中每个服务器或 SAN 阵列的多个磁盘故障。 如果没有在每个服务器或 SAN 阵列的多个磁盘故障，你可以继续执行下一步之前修复磁盘故障。 请务必请联系 Microsoft 支持，以尽可能快地解决磁盘故障。  
  
2.  以设备域管理员身份登录到 VMM 虚拟机。  
  
3.  启动配置向导。  
  
    #### <a name="to-launch-the-configuration-wizard"></a>若要启动配置向导  
  
    1.  在**服务器管理器仪表板**上**工具**菜单上，单击**Windows Server Update Services**。  
  
    2.  在左窗格中**Update Services**窗口中，单击以展开的虚拟机管理节点服务器 (***appliance_domain *-VMM**)，然后单击**选项**。  
  
    3.  在**选项**窗格中，单击**WSUS 服务器配置向导**以启动配置向导。  
  
        ![服务器管理器仪表板菜单](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  如果这是首次运行 WSUS 向导后，您可能需要配置存储更新的目录。 `C:\wsus` 是适当的位置;但是，您可以提供不同的路径。  
  
        ![WSUS 路径](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  查看**开始之前**要完成之前完成该向导的项的列表。  
  
        ![在开始之前的 WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  上**加入 Microsoft 更新改善计划**页上，选择**是，我想要加入 Microsoft 更新改善计划**，然后单击**下一步**。  
  
        ![WSUS 改善计划](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    现在，你应看到**选择上游服务器**页。 下面的屏幕截图是配置向导的起始点。  
  
    ![WSUS 上游服务器同步](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  选择上游服务器。  
  
    上**选择上游服务器**页上的 WSUS 配置向导中，你将选择的虚拟机管理节点上的 WSUS 将如何连接到上游服务器以获取软件更新。 两个可用的选项有要同步的上游服务器[Microsoft Update](http://go.microsoft.com/fwlink/?LinkId=133349)或与另一台 Windows Server Update Services 服务器中同步更新。  
  
    #### <a name="to-update-by-using-microsoft-update"></a>通过使用 Microsoft 更新来更新  
  
    1.  如果你选择使用 Microsoft Update 同步，你不需要进行任何更改到**选择上游服务器**页。 单击“下一步” 。  
  
        ![WSUS 上游服务器同步](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>若要从另一台 WSUS 服务器进行更新  
  
    1.  如果你选择将与 Microsoft 更新 （上游服务器） 以外的源同步，指定的服务器 （输入的 IP 地址） 和在其此服务器将与上游服务器通信的端口。  
  
        ![WSUS 上游服务器同步的 WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  若要使用安全套接字层 (SSL)，选择**同步更新信息时使用 SSL**复选框。 在这种情况下服务器将使用端口 443 进行同步。  
  
        ![WSUS 上游服务器同步的 WSUS SSL](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  如果这是副本服务器，选择**这是上游服务器的副本**复选框。 可以选择这两个**同步更新信息时使用 SSL**和**这是上游服务器的副本**。  
  
        ![WSUS 上游服务器副本](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  此时，您已完成与上游服务器配置。 单击**下一步**，或选择**指定代理服务器**左侧的导航窗格中。  
  
5.  指定代理服务器。  
  
    如果此服务器需要代理服务器，若要访问 Microsoft 更新或不同的上游服务器，你可以配置代理服务器设置此处;否则，请单击**下一步**。  
  
    ![WSUS Proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>若要配置代理服务器设置  
  
    1.  上**指定代理服务器**页的配置向导中，选择**同步时使用代理服务器**复选框，，然后键入代理服务器 IP 地址 （而不是名称） 和端口号 （端口 80默认值） 在对应的框。  
  
    2.  如果你想要通过使用特定用户凭据，选择连接到代理服务器**用户凭据用于连接到代理服务器**复选框，并相应然后键入用户名、 域和用户的密码框。 如果你想要启用基本身份验证将用户连接到代理服务器，选择**允许基本身份验证 （以明文形式发送密码）**复选框。  
  
        ![WSUS 代理凭据](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  此时，你就完成了代理服务器配置。 单击**下一步**转到下一页上，你可以开始设置同步过程。  
  
6.  启动连接。  
  
    ![WSUS 代理启动连接](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    单击**启动连接**。  
  
    已成功连接后，单击**下一步**转到下一页上，你可以在其中选择语言。  
  
7.  选择语言。  
  
    选择**下载这些语言的更新仅**。  
  
    选择**英语**，然后单击**下一步**。  
  
    ![选择语言](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  选择产品。  
  
    > [!NOTE]  
    > 如果使用上游服务器，你可能无法对选择的产品。 如果此选项不可用，跳过此步骤。  
  
    取消选择所有所选的更新。  
  
    选择**SQL Server 2014**， **SQL Server 2016**， **Windows Server 2012 R2**，和**System Center 2012 R2 Virtual Machine Manager**，和然后单击**下一步**。  
  
9. 选择分类。  
  
    > [!NOTE]  
    > 如果使用上游服务器，你可能无法对选择的分类。  如果此选项不可用，跳过此步骤。  
  
    取消选择所有以前选择的更新。  
  
    选择**关键更新**和**安全更新**的更新，将同步针对分析平台系统设备，然后单击**下一步**。  
  
    ![选择分类](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. 配置同步计划。  
  
    选择**手动同步**，然后单击**下一步**。  
  
    ![设置同步计划](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. 开始初始同步。  
  
    选择**开始初始同步**，然后单击**下一步**。  
  
12. 完成。  
  
    单击 **“完成”**。  
  
## <a name="bkmk_WSUSGroup"></a>组 WSUS 中的设备服务器  
之后将 WSUS 配置为 Analytics Platform System 下, 一步是进行分组的设备服务器。 通过将所有设备服务器添加到组中，WSUS 将能够将软件更新应用于设备中的所有服务器。  
  
> [!NOTE]  
> WSUS 系统旨在以异步方式运行。 启动活动不会始终导致立即更新。 因此，你可能需要等待一段时间，直到计算机将显示在 WSUS 对话框。 运行`setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"`命令在本主题末尾进行介绍[下载和应用 Microsoft 更新&#40;Analytics Platform System&#41; ](download-and-apply-microsoft-updates.md)有助于刷新的对话框。  
  
#### <a name="to-group-the-appliance-servers"></a>若要进行分组的设备服务器  
  
1.  打开 WSUS 控制台中，右键单击**所有计算机**，然后单击**添加计算机组**。  
  
    ![添加计算机组。] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  输入计算机组的名称"AP"，然后单击**添加**。  
  
    ![输入你的新计算机组的名称。] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  单击**所有计算机**同样，更改中的状态**状态**下拉列表菜单**任何**，然后单击**刷新**。 你可能需要展开**所有计算机**通过单击它才能看到新的组上左侧的树控件你刚添加。  
  
    ![将状态更改为任何并单击刷新。] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  选择所有计算机的设备，右键单击，，然后单击属于**更改成员身份**。  
  
    ![更改所有 PDW 计算机成员身份。] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  选择你通过单击复选框，然后单击创建的新计算机组**确定**。  
  
    ![设置计算机组成员身份](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  选择新的计算机组，将更改其**状态**到**任何**，然后单击**刷新**。 现在应分配给此组并在右窗格中列出的所有计算机。 它是通常可以安全地继续时节点显示警告，例如**此节点尚未尚未报告状态**。  
  
    ![将状态更改为任何并单击刷新。] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
  
