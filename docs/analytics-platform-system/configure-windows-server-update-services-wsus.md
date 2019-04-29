---
title: 配置 WSUS 的分析平台系统 |Microsoft Docs
description: 这些说明将引导你完成使用 Windows Server Update Services (WSUS) 配置向导以配置 WSUS 以分析平台系统的步骤。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 776859eb291004431a7e4e2743f1c008a7b752dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63134749"
---
# <a name="configure-windows-server-update-services-wsus-in-analytics-platform-system"></a>在分析平台系统中配置 Windows Server Update Services (WSUS)
这些说明将引导你完成使用 Windows Server Update Services (WSUS) 配置向导以配置 WSUS 以分析平台系统的步骤。 你需要先将软件更新应用到该设备配置 WSUS。 VMM 虚拟机的设备上已安装 WSUS。  
  
有关将 WSUS 配置的详细信息，请参阅[WSUS 循序渐进安装指南](https://go.microsoft.com/fwlink/?LinkId=202417)WSUS 网站上。 后配置 WSUS，请参阅[下载和应用 Microsoft 更新&#40;Analytics Platform System&#41; ](download-and-apply-microsoft-updates.md)若要启动的更新。  
  
> [!WARNING]  
> 如果在此配置过程中遇到任何错误，停止并联系支持人员获取帮助。 不要忽略错误或接收到错误后继续在进程中。  
  
## <a name="before-you-begin"></a>开始之前  
若要配置 WSUS，需要：  
  
-   具有 Analytics Platform System 设备域管理员帐户登录信息。  
  
-   有权访问的分析平台系统登录**管理员控制台**并查看设备状态信息。  
  
-   如果想要从上游 WSUS 服务器而不是同步更新直接从 Microsoft Update 同步更新，知道上游 WSUS 服务器的 IP 地址。 请确保在上游 WSUS 服务器设置为允许匿名连接，并支持 SSL。  
  
-   如果你的设备将使用代理服务器访问的上游服务器或 Microsoft Update，知道代理服务器的 IP 地址。  
  
-   在大多数情况下，WSUS 需要访问设备外的服务器。 若要支持这种分析平台系统 DNS 可以配置为支持将允许使用外部 DNS 服务器解析名称分析平台系统主机和虚拟机 (Vm) 的外部名称转发器之外的使用方案设备。 有关详细信息，请参阅[使用 DNS 转发器解析非设备 DNS 名称&#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)。  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>若要配置 Windows Server Update Services (WSUS)  
  
1.  登录到**管理员控制台**。 上**设备状态**选项卡上，确认**群集**并**网络**列显示绿色 (或**NA**) 的所有节点。 在验证所有节点的状态指示符**装置状态更改为**。  
  
    -   它可以安全地继续绿色或 NA 指示器。  
  
    -   非关键 （黄色） 警告错误的计算结果。 在某些情况下警告消息不会阻止更新。 如果不在 C:\ 驱动器的非关键磁盘卷错误，就可以解决磁盘卷错误前继续执行下一步。  
  
    -   继续操作之前，必须解决大多数的红色指示器。 如果磁盘故障，请使用**管理员控制台警报**页后，可以验证每个服务器或 SAN 阵列中的多个磁盘故障。 如果每个服务器或 SAN 阵列中的多个磁盘故障，你可以继续执行下一步之前修复磁盘故障。 请务必联系 Microsoft 支持部门以尽可能快地修复磁盘故障。  
  
2.  以设备域管理员身份登录到 VMM 虚拟机。  
  
3.  启动配置向导。  
  
    #### <a name="to-launch-the-configuration-wizard"></a>若要启动配置向导  
  
    1.  在中**服务器管理器仪表板**，然后在**工具**菜单中，单击**Windows Server Update Services**。  
  
    2.  在左窗格中**Update Services**窗口中，单击以展开的虚拟机管理节点服务器 (**_appliance_domain_VMM**)，然后单击**选项**。  
  
    3.  在中**选项**窗格中，单击**WSUS 服务器配置向导**以启动配置向导。  
  
        ![服务器管理器仪表板菜单](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  如果这是首次运行 WSUS 向导，您可能需要配置存储更新的目录。 `C:\wsus` 是一个合适的位置;但是，你可以提供不同的路径。  
  
        ![WSUS 路径](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  审阅**开始之前**要完成该向导之前，请完成的项列表。  
  
        ![WSUS 开始之前](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  上**加入 Microsoft 更新改善计划**页上，选择**是的我想要加入 Microsoft 更新改善计划**，然后单击**下一步**。  
  
        ![WSUS 改进计划](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    现在应看到**选择上游服务器**页。 下面的屏幕截图是配置向导的起始点。  
  
    ![WSUS 上游服务器同步](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  选择上游服务器。  
  
    上**选择上游服务器**页上的 WSUS 配置向导中，将选择的虚拟机管理节点上的 WSUS 将如何连接到上游服务器以获取软件更新。 两种选择是要同步的上游服务器[Microsoft Update](https://go.microsoft.com/fwlink/?LinkId=133349)或另一台 Windows Server Update Services 服务器与同步更新。  
  
    #### <a name="to-update-by-using-microsoft-update"></a>通过使用 Microsoft 更新来更新  
  
    1.  如果选择使用 Microsoft Update 同步，不需要任何更改**选择上游服务器**页。 单击“下一步” 。  
  
        ![WSUS 上游服务器同步](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>若要从另一台 WSUS 服务器更新  
  
    1.  如果选择与 Microsoft 更新 （上游服务器） 以外的源进行同步，指定的服务器 （输入的 IP 地址） 和在其此服务器将与上游服务器通信的端口。  
  
        ![WSUS 上游服务器从 WSUS 同步](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  若要使用安全套接字层 (SSL)，选择**同步更新信息时使用 SSL**复选框。 在这种情况下服务器将使用端口 443 进行同步。  
  
        ![WSUS 上游服务器从 WSUS SSL 同步](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  如果副本服务器，请选择**这是上游服务器副本**复选框。 可以选择这两个**同步更新信息时使用 SSL**并**这是上游服务器副本**。  
  
        ![WSUS 上游服务器副本](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  此时，已完成与上游服务器配置。 单击**下一步**，或选择**指定代理服务器**左侧的导航窗格中。  
  
5.  指定代理服务器。  
  
    如果此服务器需要代理服务器，若要访问 Microsoft 更新或其他上游服务器，可以配置代理服务器设置否则，请单击**下一步**。  
  
    ![WSUS Proxy](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>若要配置代理服务器设置  
  
    1.  上**指定代理服务器**配置向导，选择页面**同步时使用代理服务器**复选框，，然后键入代理服务器 IP 地址 （而不是名称） 和端口号 （80 情况下为端口默认值） 对应的框。  
  
    2.  如果你想要使用特定用户凭据，选择连接到代理服务器**使用用户凭据来连接到代理服务器**复选框，然后相应然后键入用户名、 域和用户的密码框。 如果你想要启用基本身份验证连接到代理服务器，选择的用户**允许基本身份验证 （密码以明文形式发送）** 复选框。  
  
        ![WSUS 代理凭据](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  此时，您就完成了代理服务器配置。 单击**下一步**转到下一页上，你可以开始设置同步过程。  
  
6.  开始连接。  
  
    ![WSUS 代理开始连接](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    单击**开始连接**。  
  
    已成功连接后，单击**下一步**以转到下一步的页中，您可以在其中选择语言。  
  
7.  选择语言。  
  
    选择**下载这些语言的更新仅**。  
  
    选择**英语**，然后单击**下一步**。  
  
    ![选择语言](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  选择产品。  
  
    > [!NOTE]  
    > 如果使用上游服务器，您可能不能选择产品。 如果此选项不可用，请跳过此步骤。  
  
    取消选择所有所选的更新。  
  
    选择**Windows Server 2012 R2**，并**System Center 2012 R2 Virtual Machine Manager**，然后单击**下一步**。  
  
9. 选择分类。  
  
    > [!NOTE]  
    > 如果使用上游服务器，你可能无法对选择类别。  如果此选项不可用，请跳过此步骤。  
  
    取消选择所有以前选择的更新。  
  
    选择**关键更新**并**安全更新**的更新，将同步的分析平台系统设备，然后单击**下一步**。  
  
    ![选择分类](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. 配置同步计划。  
  
    选择**手动同步**，然后单击**下一步**。  
  
    ![设置同步计划](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. 开始初始同步。  
  
    选择**开始初始同步**，然后单击**下一步**。  
  
12. 完成。  
  
    单击 **“完成”**。  
  
## <a name="bkmk_WSUSGroup"></a>在 WSUS 中的设备服务器组合  
Analytics Platform system 配置 WSUS 之后, 的下一步是进行分组的设备服务器。 通过将所有设备服务器添加到组，WSUS 将能够将软件更新应用到设备中的所有服务器。  
  
> [!NOTE]  
> WSUS 系统旨在以异步方式运行。 启动活动不会始终导致立即更新。 因此，您可能需要等待一段时间，直到计算机会在 WSUS 对话框框中显示。 运行`setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"`命令在该主题的结尾所述[下载和应用 Microsoft 更新&#40;Analytics Platform System&#41; ](download-and-apply-microsoft-updates.md)有助于刷新访问的对话框。  
  
#### <a name="to-group-the-appliance-servers"></a>若要进行分组的设备服务器  
  
1.  打开 WSUS 控制台中，右键单击**的所有计算机**，然后单击**添加计算机组**。  
  
    ![添加计算机组。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  输入计算机组的名称"AP"，然后单击**添加**。  
  
    ![输入你的新计算机组的名称。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  单击**的所有计算机**同样，更改中的状态**状态**下拉列表菜单**任何**，然后单击**刷新**。 可能需要展开**的所有计算机**单击它才能看到新的组在左侧树控件您只需添加了。  
  
    ![将状态更改为任何并单击刷新。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  选择所有计算机的一部分的设备，右键单击，再单击**更改成员身份**。  
  
    ![更改所有 PDW 计算机的成员身份。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  选择通过单击复选框，然后单击创建的新计算机组**确定**。  
  
    ![设置计算机组成员身份](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  选择新的计算机组，更改其**状态**到**任何**，然后单击**刷新**。 现在应分配给此组并在右窗格中列出的所有计算机。 它是通常可以安全地继续时节点显示警告，例如**此节点状态尚未报告**。  
  
    ![将状态更改为任何并单击刷新。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
  
