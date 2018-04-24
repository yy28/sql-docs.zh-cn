---
title: 配置分析平台系统的 InfiniBand-|Microsoft 文档
description: 描述如何在要连接到控制节点上并行数据仓库 (PDW) 的非设备客户端服务器上配置无线带宽技术网络适配器。 基本连接性和高可用性，以便加载、 备份、 和其他进程自动连接到活动的无限带宽网络内容，请使用这些说明。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 8e67d63e7bb4bded0bd19e5db4a0b7faddb80977
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>为分析平台系统配置无线带宽技术网络适配器
描述如何在要连接到控制节点上并行数据仓库 (PDW) 的非设备客户端服务器上配置无线带宽技术网络适配器。 基本连接性和高可用性，以便加载、 备份、 和其他进程自动连接到活动的无限带宽网络内容，请使用这些说明。  
  
## <a name="Basics"></a>说明  
这些说明显示了如何查找，然后正确 InfiniBand IP 地址和子网掩码服务器上设置 InfiniBand 连接。 它们还介绍了如何设置你的服务器以使用 AP 设备 DNS，以便你在连接解析到的活动的 InfiniBand 网络。  
  
对于高可用性，AP 具有两个 InfiniBand 网络、 1 个活动和一个被动。 每个 InfiniBand 网络有控制节点有关的其他 IP 地址。 如果活动的 InfiniBand 网络出现故障，被动 InfiniBand 网络将成为活动的网络。 当发生这种情况的脚本或进程自动连接到活动的 InfiniBand 网络而无需更改脚本参数。  
  
具体而言，在此文章你：  
  
1.  查找服务器的 AP DNS 的 InfiniBand IP 地址 (appliance_domain AD01 和 appliance_domain *-AD02)。 若要这样做你登录到 AD01 和 AD02 服务器，并为每个 InfiniBand 网络获得 IP 地址。 AD 节点上的 InfiniBand IP 地址的 DNS IP 地址的。  
  
2.  每个网络适配器配置为使用 AP 无限带宽网络上可用的 IP 地址。  
  
    1.  如果你有两个 InfiniBand 网络适配器，你可以使用这第二个 InfiniBand 网络称为 TeamIB2 称为 TeamIB1 和可用的 IP 地址的其他适配器的第一个 InfiniBand 网络中可用的 IP 地址配置一个适配器。 使用 appliance_domain AD01 TeamIB1 IP 地址作为首选的 DNS 服务器和 appliance_domain AD02 TeamIB1 为 TeamIB1 网络适配器的备用 DNS 服务器的 IP 地址。 使用 appliance_domain AD01 TeamIB2 IP 地址作为首选的 DNS 服务器和 appliance_domain AD02 TeamIB2 为 TeamIB2 网络适配器的备用 DNS 服务器的 IP 地址。  
  
    2.  如果必须只有一个 InfiniBand 网络适配器，你可以使用从一个 InfiniBand 网络可用的 IP 地址配置适配器。 然后你会在使用 appliance_domain AD01 TeamIB1 和 appliance_domain AD02 TeamIB1 或使用者为准位于相同 appliance_domain AD01 TeamIB2 和 appliance_domain AD02 TeamIB2 此适配器上配置首选和备用 DNS 服务器分别作为配置的适配器作为首选和备用 DNS 服务器的网络。  
  
3.  配置无线带宽技术网络适配器以使用 AP DNS 服务器解析你的连接为活动的 InfiniBand 网络。  
  
    1.  若要配置此高级的 TCP/IP 设置用于将设备域 DNS 后缀添加到 DNS 后缀的列表的开头，客户端服务器上。 此操作仅需在一个网络适配器中; 上配置设置适用于这两个适配器。  
  
在配置你的无线带宽技术网络适配器后，客户端进程可以使用连接到无限带宽网络上的控件节点`PDW_region-SQLCTL01`服务器的地址。 你的服务器将追加分析平台系统 DNS 后缀，也可以输入的完整地址，即`PDW_region-SQLCTL01.appliance_domain.pdw.local`。  
  
例如，如果你 PDW 地区名称都是 MyPDW 和设备名称是 MyAPS，加载数据的 dwloader 服务器规范是以下项之一：  
  
-   `dwloader –S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader –S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>开始之前  
  
### <a name="requirements"></a>需求  
你需要 AP 设备的域帐户，登录到 AD01 节点。 例如，F12345 * \Administrator。  
  
你需要有权配置的网络适配器的客户端服务器上的 Windows 帐户。  
  
### <a name="prerequisites"></a>必要條件  
这些说明假定客户端服务器已架装并连接好电缆，到设备 InfiniBand 网络。 有关安装和电缆连接说明，请参阅[获取和配置加载服务器](acquire-and-configure-loading-server.md)。  
  
### <a name="general-remarks"></a>一般备注  
通过使用 SQLCTL01，分析平台系统 DNS 客户端服务器的控件节点通过使用连接到活动的 InfiniBand 网络。 这仅适用于获取连接;如果在加载或备份期间，InfiniBand 网络出现故障，你需要重新启动此过程。  
  
要根据业务需求，还可以加入到你自己的非设备工作组或 Windows 域的客户端服务器。  
  
## <a name="Sec1"></a>步骤 1： 获取设备 InfiniBand 网络设置  
*要获取 InfiniBand 网络设置的设备*  
  
1.  登录到该设备 AD01 节点使用 appliance_domain\Administrator 帐户。  
  
2.  在设备 AD01 节点上，打开控制面板，选择网络和 Internet、 选择网络和共享中心 *，，然后选择更改适配器设置。  
  
3.  在网络连接窗口中，右键单击团队 IB1，然后选择属性。  
  
    ![无限带宽连接的管理节点上](media/network-teamib.png "InfiniBand 连接的管理节点上")  
  
4.  从 Internet 协议版本 4 (TCP/IPv4) 属性窗口中，记下的值**IP 地址**和**子网掩码**。  IP 地址 ***appliance_domain *-AD01**节点是分析平台系统 DNS 服务器的 IP 地址。  
  
5.  上重复步骤 1-5 上述 TeamIB1 适配器 ***appliance_domain *-AD02**服务器。  
  
    ![PDW 管理节点 InfiniBand 1 属性](media/network-ip1-properties.png "PDW 管理节点 InfiniBand 1 属性")  
  
6.  单击取消以关闭该窗口。  
  
7.  TeamIB1 网络上查找未使用的 IP 地址并将其记下。  
  
    若要查找未使用的 IP 地址，请打开命令窗口并尝试 ping 你的设备的地址的范围内的 IP 地址。 在此示例中，TeamIB1 网络的 IP 地址是 172.16.14.30。 查找开头 172.16.14 未使用的 IP 地址。 例如，从命令行中输入"ping 172.16.14.254"。 如果 ping 请求失败，是可用的 IP 地址。  
  
8.  有关 TeamIB2 执行相同的操作。 在 * 网络连接窗口中，团队 IB2 右键单击并选择属性。  
  
9. 从 Internet 协议版本 4 (TCP/IPv4) 属性窗口中，记下 IP 地址和子网掩码的值为 TeamIB2。  
  
10. 对 appliance_domain AD02 服务器上的 TeamIB2 适配器重复步骤 8-9 上面。  
  
    ![属性 TeamIB2](media/network-ip2-properties.png "TeamIB2 属性")  
  
11. 找到未使用的 IP 地址**TeamIB2**网络，然后将其记下。  
  
    若要查找未使用的 IP 地址，请打开命令窗口并尝试 ping 你的设备的地址的范围内的 IP 地址。 在此示例中，TeamIB2 网络的 IP 地址是 172.16.18.30。 查找开头 172.16.18 未使用的 IP 地址。 例如，从命令行中输入"ping 172.16.18.254"。 如果 ping 请求失败，是可用的 IP 地址。  
  
## <a name="Sec2"></a>步骤 2： 客户端服务器上配置无线带宽技术网络适配器设置  

### <a name="notes"></a>说明  
  
-   这些步骤演示了如何使用 AP DNS 服务器注册你的服务器。  
  
-   为了满足你自己的网络要求，您还可以为你自己的非设备工作组或 Windows 域加入客户端服务器。  
  
-   说明单步执行每个服务器上配置两个网络适配器。  如果你只有一个网络适配器，选择其中一个网络网络适配器上配置，然后将第二个 DNS IP 地址添加为备用 DNS 服务器。  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>若要在客户端服务器上配置无线带宽技术网络适配器设置  
  
1.  以 Windows 管理员身份登录到你加载、 备份或其他设备上的客户端服务器 InfiniBand 网络。  
  
2.  打开控件窗格 *，选择网络和共享中心，然后选择更改适配器设置。  
  
### <a name="to-configure-the-first-network-adapter"></a>若要配置的第一个网络适配器  
  
1.  在网络连接窗口中，右键单击其中一个无法识别的网络槽 Mellanox 适配器，然后选择属性。  
  
    ![选择 InfiniBand 网络](media/network-connections.png "选择 InfiniBand 网络")  
  
2.  在属性窗口  
  
    1.  在常规选项卡上，将该 IP 地址设置验证为 TeamIB1 ping 测试中可用的 IP 地址。 本文中使用的示例值，则将输入 172.16.14.254。  
  
    2.  将子网掩码设置为你为 TeamIB1 记下的子网掩码。  
  
    3.  将首选 DNS 服务器设置为 TeamIB1 从 appliance_domain * 前面记下的 IP 地址-AD01 节点。  
  
    4.  将备用 DNS 服务器设置为 TeamIB1 从 appliance_domain * 前面记下的 IP 地址-AD02 节点。  
  
        ![InfiniBand 1 个网络适配器属性](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  单击确定以应用更改。  
  
### <a name="to-configure-the-second-network-adapter"></a>若要配置的第二个网络适配器  
  
1.  如果你只有一个网络适配器，跳过此部分。  
  
2.  在网络连接窗口中，右键单击第二个未识别的网络段上为 Mellanox 适配器，然后选择属性。  
  
    ![选择 InfiniBand 网络](media/network-connections.png "选择 InfiniBand 网络")  
  
3.  在属性窗口  
  
    1.  在常规选项卡上，将该 IP 地址设置验证为 TeamIB2 ping 测试中可用的 IP 地址。 本文中使用的示例值，则将输入 172.16.18.254。  
  
    2.  将子网掩码设置为你为 TeamIB2 记下的子网掩码。  
  
    3.  将首选 DNS 服务器设置为 TeamIB2 从 appliance_domain * 前面记下的 IP 地址-AD01 节点。  
  
    4.  将备用 DNS 服务器设置为 TeamIB2 从 appliance_domain * 前面记下的 IP 地址-AD02 节点。  
  
        > [!NOTE]  
        > 如果你只有一个网络适配器，请配置首选和备用 DNS 服务器分别作为首选和备用 DNS 服务器使用的设备 AD01 TeamIB1 和设备 AD02 TeamIB1 或使用设备 AD01 TeamIB2 和设备 AD02 TeamIB2 作为首选和备用的 DNS 服务器，具体取决于 AD 虚拟机已故障转移。  
  
        ![InfiniBand 1 个网络适配器属性](media/network-ib1-properties.png "InfiniBand 1 个网络适配器属性")  
  
    5.  单击确定以应用更改。  
  
### <a name="to-configure-the-dns-suffix"></a>若要配置的 DNS 后缀  
  
1.  在网络连接窗口中，右键单击其中一个网络槽 Mellanox 适配器，然后选择属性。  
  
2.  单击高级... 按钮。  
  
3.  在高级 TCP/IP 设置窗口中，如果追加这些 DNS 后缀 （按顺序） 选项并不灰显，复选框称为追加这些 DNS 后缀 （按顺序）:，选择设备域后缀，然后单击添加... 设备域后缀是 `appliance_domain.local`  
  
4.  如果附加这些 DNS 后缀 （按顺序）： 选项灰显，你可以通过修改注册表项 HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient AP 域添加到此服务器。  
  
    ![TCP/IP 设置](media/network-tcpip.png "TCP/IP 设置")  
  
5.  对于更快的地址解析，我们建议将设备后缀移至列表顶部。  
  
6.  单击“确定”。  
  
7.  现在，你可以使用连接到设备 Infiniband 网络`PDW_region-SQLCTL01.appliance_domain.local`，或只需`appliance_domain-SQLCTL01`。 如果使用的完整名称和 DNS 后缀来连接可能更快地建立的连接。  
  
    设备的示例名 MyAPS 为与 MyPDW PDW 区域：  
  
    -   MyPDW-SQLCTL01.MyAPS.local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>另请参阅  
[获取和配置加载服务器 ](acquire-and-configure-loading-server.md)  
  
