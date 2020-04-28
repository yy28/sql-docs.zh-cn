---
title: 配置未配置
description: 描述如何在非设备客户端服务器上配置不使用的网络适配器以连接到并行数据仓库（PDW）上的控制节点。 对于基本连接和高可用性，请使用这些说明，以便加载、备份和其他进程自动连接到活动的未占用网络。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 583d7617c0620d5d1ec24d60fbf10435a547616d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401295"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>为分析平台系统配置无线网络适配器
描述如何在非设备客户端服务器上配置不使用的网络适配器以连接到并行数据仓库（PDW）上的控制节点。 对于基本连接和高可用性，请使用这些说明，以便加载、备份和其他进程自动连接到活动的未占用网络。  
  
## <a name="description"></a><a name="Basics"></a>说明  
这些说明显示了如何查找并在未连接的服务器上设置正确的可操作 IP 地址和子网掩码。 它们还介绍了如何将服务器设置为使用 AP 设备 DNS，以便将连接解析为活动的未占用网络。  
  
为实现高可用性，AP 有两个未经过的网络，一个处于活动状态，一个是被动网络。 每个未使用的网络对于控制节点具有不同的 IP 地址。 如果处于活动状态的网络中断，则被动的 "停止" 网络将成为活动网络。 如果出现这种情况，则脚本或进程会自动连接到活动的自动连接网络，而不会更改脚本参数。  
  
具体而言，在本文中，你将：  
  
1.  查找接入点 DNS 服务器（appliance_domain-AD01 和 appliance_domain *-AD02）的不确定的 IP 地址。 为此，请登录到 AD01 和 AD02 服务器，并获取每个未完成网络的 IP 地址。 AD 节点上的未处理 IP 地址是 DNS IP 地址。  
  
2.  将每个网络适配器配置为使用 "AP 无网络" 网络上的可用 IP 地址。  
  
    1.  如果有两个不符合要求的网络适配器，则可以在第一次不使用的网络（称为 TeamIB1）中配置一个具有可用 ip 地址的适配器，在第二个未处理的网络（称为 TeamIB2）中配置另一个适配器。 使用 appliance_domain-AD01 TeamIB1 IP 地址作为首选 DNS 服务器，并 appliance_domain-AD02 TeamIB1 IP 地址作为 TeamIB1 网络适配器的备用 DNS 服务器。 使用 appliance_domain-AD01 TeamIB2 IP 地址作为首选 DNS 服务器，并 appliance_domain-AD02 TeamIB2 IP 地址作为 TeamIB2 网络适配器的备用 DNS 服务器。  
  
    2.  如果只有一个未受支持的网络适配器，则可以使用其中一个不受阻止的网络来配置具有可用 IP 地址的适配器。 然后，使用 appliance_domain-AD01 TeamIB1 和 appliance_domain-AD02 TeamIB1 或使用 appliance_domain-AD01 TeamIB2 和 appliance_domain-AD02 TeamIB2 （与配置的适配器在同一网络上分别作为首选和备用 DNS 服务器）配置此适配器上的首选和备用 DNS 服务器。  
  
3.  配置不使用的网络适配器，以使用接入点 DNS 服务器来解析到活动的未占用网络的连接。  
  
    1.  若要对此进行配置，请使用 "高级 TCP/IP 设置" 将 "设备域 DNS 后缀" 添加到客户端服务器上 DNS 后缀列表的开头。 这只需要在一个网络适配器上进行配置;此设置适用于这两个适配器。  
  
在配置未受管理的网络适配器之后，客户端进程可以通过使用`PDW_region-SQLCTL01`为服务器地址连接到可管理的网络上的控制节点。 你的服务器将追加分析平台系统 DNS 后缀，也可以输入完整的地址`PDW_region-SQLCTL01.appliance_domain.pdw.local`。  
  
例如，如果 PDW 区域名称为 MyPDW 并且设备名称为 MyAPS，则用于加载数据的 dwloader 服务器规范为以下其中一项：  
  
-   `dwloader -S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader -S MYPDW-SQLCTL01`  
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>开始之前  
  
### <a name="requirements"></a>要求  
需要使用一个 AP 设备帐户登录到 AD01 节点。 例如，F12345 * \Administrator。  
  
你需要客户端服务器上有权配置网络适配器的 Windows 帐户。  
  
### <a name="prerequisites"></a>先决条件  
这些说明假定已经装好客户端服务器并将其连接到设备的 "无线网络"。 有关搭架和布线的说明，请参阅[获取和配置加载服务器](acquire-and-configure-loading-server.md)。  
  
### <a name="general-remarks"></a>一般备注  
通过使用 SQLCTL01，分析平台系统 DNS 使用活动的未受管理网络将客户端服务器连接到控制节点。 这仅适用于连接;如果负载或备份过程中的 "未使用" 网络停机，则需要重新启动该进程。  
  
为了满足你自己的业务要求，你还可以将客户端服务器加入你自己的非设备工作组或 Windows 域。  
  
## <a name="step-1-obtain-the-appliance-infiniband-network-settings"></a><a name="Sec1"></a>步骤1：获取设备不会的网络设置  
*获取设备不会的网络设置*  
  
1.  使用 appliance_domain \Administrator 帐户登录到装置 AD01 节点。  
  
2.  在 "设备 AD01" 节点上，打开 "控制面板"，选择 "网络和 Internet"，选择 "网络和共享中心"，然后选择 "更改适配器设置"。  
  
3.  在 "网络连接" 窗口中，右键单击 "Team IB1"，然后选择 "属性"。  
  
    ![管理节点上的未管理连接](media/network-teamib.png "管理节点上的未管理连接")  
  
4.  在 "Internet 协议版本4（TCP/IPv4）" 属性窗口中，记下 " **IP 地址**" 和 "**子网掩码**" 的值。  **_设备\_域_-AD01**节点的 IP 地址是分析平台系统 DNS 服务器的 ip 地址。  
  
5.  为**_设备\__** 上的 TeamIB1 适配器重复步骤 1-5-AD02 服务器。  
  
    ![PDW 管理节点无限1属性](media/network-ip1-properties.png "PDW 管理节点无限1属性")  
  
6.  单击“取消”可关闭窗口。  
  
7.  在 TeamIB1 网络上查找未使用的 IP 地址，并将其记下。  
  
    若要查找未使用的 IP 地址，请打开命令窗口，尝试对设备的地址范围内的 IP 地址进行 ping 操作。 在此示例中，TeamIB1 网络的 IP 地址为172.16.14.30。 查找以 "172.16.14" 开头但未使用的 IP 地址。 例如，在命令行中输入 "ping 172.16.14.254"。 如果 ping 请求失败，则 IP 地址可用。  
  
8.  为 TeamIB2 执行相同的操作。 在 "网络连接" 窗口中，右键单击 "Team IB2"，然后选择 "属性"。  
  
9. 从 Internet 协议版本4（TCP/IPv4）属性窗口中，记下 TeamIB2 的 IP 地址和子网掩码的值。  
  
10. 对于 appliance_domain-AD02 服务器上的 TeamIB2 适配器，请重复上述步骤8-9。  
  
    ![TeamIB2 的属性](media/network-ip2-properties.png "TeamIB2 的属性")  
  
11. 在**TeamIB2**网络上查找未使用的 IP 地址，并将其记下。  
  
    若要查找未使用的 IP 地址，请打开命令窗口，尝试对设备的地址范围内的 IP 地址进行 ping 操作。 在此示例中，TeamIB2 网络的 IP 地址为172.16.18.30。 查找以 "172.16.18" 开头但未使用的 IP 地址。 例如，在命令行中输入 "ping 172.16.18.254"。 如果 ping 请求失败，则 IP 地址可用。  
  
## <a name="step-2-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a><a name="Sec2"></a>步骤2：在客户端服务器上配置不工作网络适配器设置  

### <a name="notes"></a>说明  
  
-   以下步骤说明如何向 AP DNS 服务器注册服务器。  
  
-   为了满足你自己的网络需求，你还可以将客户端服务器加入你自己的非设备工作组或 Windows 域。  
  
-   说明步骤介绍了如何在每个服务器上配置两个网络适配器。  如果只有一个网络适配器，请选择要在网络适配器上配置的网络之一，然后将第二个 DNS IP 地址添加为备用 DNS 服务器。  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>在客户端服务器上配置不工作网络适配器设置  
  
1.  以 Windows 管理员身份登录到设备上的加载、备份或其他客户端服务器。  
  
2.  打开 "控件" 窗格，选择 "网络和共享中心"，然后选择 "更改适配器设置"。  
  
### <a name="to-configure-the-first-network-adapter"></a>配置第一个网络适配器  
  
1.  在 "网络连接" 窗口中，右键单击用于 Mellanox 适配器的一个未识别的网络槽，然后选择 "属性"。  
  
    ![选择 InfiniBand 网络](media/network-connections.png "选择 InfiniBand 网络")  
  
2.  在属性窗口  
  
    1.  在 "常规" 选项卡上，将 IP 地址设置为在 TeamIB1 的 ping 测试中验证为 "可用" 的 IP 地址。 对于本文中使用的示例值，请输入172.16.14.254。  
  
    2.  将子网掩码设置为你为 TeamIB1 记下的子网掩码。  
  
    3.  将首选 DNS 服务器设置为之前从 appliance_domain *-AD01 节点记下的 TeamIB1 的 IP 地址。  
  
    4.  将备用 DNS 服务器设置为之前从 appliance_domain *-AD02 节点中记下的 TeamIB1 的 IP 地址。  
  
        ![无限1网络适配器属性](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  单击“确定”以应用更改。  
  
### <a name="to-configure-the-second-network-adapter"></a>配置第二个网络适配器  
  
1.  如果只有一个网络适配器，请跳过此部分。  
  
2.  在 "网络连接" 窗口中，右键单击 "Mellanox 适配器" 的第二个 "未识别的网络" 插槽，然后选择 "属性"。  
  
    ![选择 InfiniBand 网络](media/network-connections.png "选择 InfiniBand 网络")  
  
3.  在属性窗口  
  
    1.  在 "常规" 选项卡上，将 IP 地址设置为在 TeamIB2 的 ping 测试中验证为 "可用" 的 IP 地址。 对于本文中使用的示例值，请输入172.16.18.254。  
  
    2.  将子网掩码设置为你为 TeamIB2 记下的子网掩码。  
  
    3.  将首选 DNS 服务器设置为之前从 appliance_domain *-AD01 节点记下的 TeamIB2 的 IP 地址。  
  
    4.  将备用 DNS 服务器设置为之前从 appliance_domain *-AD02 节点中记下的 TeamIB2 的 IP 地址。  
  
        > [!NOTE]  
        > 如果只有一个网络适配器，请使用设备 AD01 TeamIB1 和设备 AD02 TeamIB1 分别配置首选和备用 DNS 服务器作为首选和备用 DNS 服务器，或者使用设备 AD01 TeamIB2 和设备 AD02 TeamIB2 作为首选和备用 DNS 服务器，具体取决于 AD 虚拟机是否已故障转移。  
  
        ![无限1网络适配器属性](media/network-ib1-properties.png "无限1网络适配器属性")  
  
    5.  单击“确定”以应用更改。  
  
### <a name="to-configure-the-dns-suffix"></a>配置 DNS 后缀  
  
1.  在 "网络连接" 窗口中，右键单击一个用于 Mellanox 适配器的网络槽，然后选择 "属性"。  
  
2.  单击 "高级 ..."鼠标.  
  
3.  在 "高级 TCP/IP 设置" 窗口中，如果 "附加这些 DNS 后缀（按顺序）" 选项未灰显，请选中名为 "附加这些 DNS 后缀（按顺序）" 的框：，选择设备的域后缀，然后单击 "添加 ..."。设备域后缀是`appliance_domain.local`  
  
4.  如果 "附加这些 DNS 后缀（按顺序）" 选项灰显，则可以通过修改注册表项 HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows NT\DNSClient. 将 AP 域添加到此服务器。  
  
    ![TCP/IP 设置](media/network-tcpip.png "TCP/IP 设置")  
  
5.  为了更快地解决地址问题，建议将设备后缀移至列表的顶部。  
  
6.  单击“确定”。  
  
7.  现在，你可以使用`PDW_region-SQLCTL01.appliance_domain.local`或简单地`appliance_domain-SQLCTL01`连接到设备的网络设备。 如果连接的是全名和 DNS 后缀，则连接速度可能更快。  
  
    名为 MyAPS 的设备的示例，MyPDW PDW 地区：  
  
    -   MyPDW-SQLCTL01. MyAPS  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>另请参阅  
[获取和配置加载服务器](acquire-and-configure-loading-server.md)  
  
