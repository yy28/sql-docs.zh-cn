---
title: 配置 InfiniBand 的分析平台系统 |Microsoft Docs
description: 介绍如何在要连接到控制节点上并行数据仓库 (PDW) 的非设备客户端服务器上配置无线带宽技术网络适配器。 使用这些指令的基本连接并以实现高可用性，以便加载、 备份以及其他进程会自动连接到活动的 InfiniBand 网络。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0421361cf1718d6ee280269f9da125c148aa3afd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518275"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>配置分析平台系统的 InfiniBand 网络适配器
介绍如何在要连接到控制节点上并行数据仓库 (PDW) 的非设备客户端服务器上配置无线带宽技术网络适配器。 使用这些指令的基本连接并以实现高可用性，以便加载、 备份以及其他进程会自动连接到活动的 InfiniBand 网络。  
  
## <a name="Basics"></a>说明  
这些说明介绍了如何查找，然后设置正确的 InfiniBand IP 地址和子网掩码在 InfiniBand 连接的服务器上。 此外介绍了如何设置你的服务器以使用 APS 设备 DNS，以便你的连接将解析为活动的 InfiniBand 网络。  
  
对于高可用性，AP 具有两个 InfiniBand 网络，只能将一个活动和一个被动。 每个 InfiniBand 网络有不同的控制节点的 IP 地址。 如果活动的 InfiniBand 网络出现故障，被动的 InfiniBand 网络将成为活动的网络。 在此情况下脚本或进程会自动连接到活动的 InfiniBand 网络而无需更改脚本参数。  
  
具体而言，在此项目您：  
  
1.  查找服务器的 APS DNS 的 InfiniBand IP 地址 (appliance_domain AD01 和 appliance_domain *-AD02)。 若要执行此操作登录到 AD01 和 AD02 服务器，并为每个 InfiniBand 网络获取 IP 地址。 AD 节点上的 InfiniBand IP 地址是 DNS IP 地址。  
  
2.  每个网络适配器配置为使用 APS InfiniBand 网络上的可用的 IP 地址。  
  
    1.  如果有两个 InfiniBand 网络适配器，则第一个称为 TeamIB1，而另一个适配器可用的 IP 地址与第二个称为 TeamIB2 的 InfiniBand 网络中的 InfiniBand 网络中的可用 IP 地址配置一个适配器。 使用 appliance_domain AD01 TeamIB1 IP 地址用作首选的 DNS 服务器和 appliance_domain AD02 TeamIB1 作为 TeamIB1 网络适配器的备用 DNS 服务器的 IP 地址。 使用 appliance_domain AD01 TeamIB2 IP 地址用作首选的 DNS 服务器和 appliance_domain AD02 TeamIB2 作为 TeamIB2 网络适配器的备用 DNS 服务器的 IP 地址。  
  
    2.  如果必须只有一个 InfiniBand 网络适配器，您可以使用 InfiniBand 网络之一中的可用 IP 地址配置适配器。 然后你会使用 appliance_domain AD01 TeamIB1 和 appliance_domain AD02 TeamIB1 或使用者为准位于相同 appliance_domain AD01 TeamIB2 和 appliance_domain AD02 TeamIB2 此适配器上配置首选和备用 DNS 服务器分别为配置的适配器为首选和备用 DNS 服务器的网络。  
  
3.  配置 InfiniBand 网络适配器以使用 APS DNS 服务器解析为活动的 InfiniBand 网络的连接。  
  
    1.  若要配置此高级的 TCP/IP 设置用于客户端服务器上将设备域 DNS 后缀添加到 DNS 后缀的列表的开头。 这只需在上一个网络适配器中; 配置设置适用于这两个适配器。  
  
配置 InfiniBand 网络适配器之后, 客户端进程可以使用连接到 InfiniBand 网络上的控件节点`PDW_region-SQLCTL01`的服务器的地址。 你的服务器将追加分析平台系统 DNS 后缀，也可以输入完整地址是`PDW_region-SQLCTL01.appliance_domain.pdw.local`。  
  
例如，如果你的 PDW 区域名称是 MyPDW，设备名称是 MyAPS dwloader 服务器规范，用于将数据加载是以下值之一：  
  
-   `dwloader -S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader -S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>开始之前  
  
### <a name="requirements"></a>要求  
你需要登录到 AD01 节点 APS 设备域帐户。 例如，F12345 * \Administrator。  
  
需要有权配置网络适配器的客户端服务器上的 Windows 帐户。  
  
### <a name="prerequisites"></a>先决条件  
这些说明假定已装入机架并连接到设备 InfiniBand 网络客户端服务器。 有关安装和布线说明，请参阅[获取和配置加载服务器](acquire-and-configure-loading-server.md)。  
  
### <a name="general-remarks"></a>一般备注  
通过使用 SQLCTL01，分析平台系统 DNS 客户端服务器使用连接到控制节点活动的 InfiniBand 网络。 这仅适用于进行连接;如果在加载或备份期间出现故障的 InfiniBand 网络，，需要重新启动该进程。  
  
要满足业务需求，还可以加入到你自己的非设备工作组或 Windows 域的客户端服务器。  
  
## <a name="Sec1"></a>步骤 1:获取装置 InfiniBand 网络设置  
*若要获取 InfiniBand 网络设置的设备*  
  
1.  登录到该设备 AD01 节点使用 appliance_domain\Administrator 帐户。  
  
2.  设备 AD01 在节点上，打开控制面板中，选择网络和 Internet、 选择网络和共享中心 *，，然后选择更改适配器设置。  
  
3.  在网络连接窗口中，右键单击团队 IB1，然后选择属性。  
  
    ![管理节点上的 InfiniBand 连接](media/network-teamib.png "管理节点上的 InfiniBand 连接")  
  
4.  从 Internet 协议版本 4 (TCP/IPv4) 属性窗口中，记下为值**IP 地址**并**子网掩码**。  IP 地址**_装置\_域_-AD01**节点是分析平台系统 DNS 服务器的 IP 地址。  
  
5.  上重复步骤 1-5 以上 TeamIB1 适配器**_装置\_域_-AD02**服务器。  
  
    ![PDW 管理节点 InfiniBand 1 属性](media/network-ip1-properties.png "PDW 管理节点 InfiniBand 1 属性")  
  
6.  单击取消以关闭该窗口。  
  
7.  TeamIB1 网络上查找未使用的 IP 地址并将其记下。  
  
    若要查找未使用的 IP 地址，请打开命令窗口并尝试执行 ping 操作的设备的地址范围内的 IP 地址。 在此示例中，TeamIB1 网络的 IP 地址是 172.16.14.30。 查找开头 172.16.14 未使用的 IP 地址。 例如，从命令行中输入"ping 172.16.14.254"。 如果 ping 请求失败，是可用的 IP 地址。  
  
8.  TeamIB2 的属性执行相同的操作。 在 * 网络连接窗口中，右键单击团队 IB2 并选择属性。  
  
9. 从 Internet 协议版本 4 (TCP/IPv4) 属性窗口中，记下 IP 地址和子网掩码的值为 TeamIB2。  
  
10. TeamIB2 适配器 appliance_domain AD02 服务器上重复步骤 8-9 更高版本。  
  
    ![TeamIB2 的属性](media/network-ip2-properties.png "TeamIB2 的属性")  
  
11. 有关未使用的 IP 地址**TeamIB2**网络，然后将其记下。  
  
    若要查找未使用的 IP 地址，请打开命令窗口并尝试执行 ping 操作的设备的地址范围内的 IP 地址。 在此示例中，TeamIB2 网络的 IP 地址是 172.16.18.30。 查找开头 172.16.18 未使用的 IP 地址。 例如，从命令行中输入"ping 172.16.18.254"。 如果 ping 请求失败，是可用的 IP 地址。  
  
## <a name="Sec2"></a>步骤 2:在客户端服务器上配置的 InfiniBand 网络适配器设置  

### <a name="notes"></a>说明  
  
-   这些步骤演示了如何使用 APS DNS 服务器注册你的服务器。  
  
-   要满足网络要求，还可以加入到你自己的非设备工作组或 Windows 域的客户端服务器。  
  
-   每个服务器上配置两个网络适配器的分步说明。  如果只有一个网络适配器，选择其中一个网络上的网络适配器，配置，然后将第二个 DNS IP 地址添加为备用 DNS 服务器。  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>若要在客户端服务器上配置的 InfiniBand 网络适配器设置  
  
1.  以 Windows 管理员身份登录到你加载、 备份或在设备上的其他客户端服务器的 InfiniBand 网络。  
  
2.  打开控制窗格 *，选择网络和共享中心，然后选择更改适配器设置。  
  
### <a name="to-configure-the-first-network-adapter"></a>若要配置的第一个网络适配器  
  
1.  在网络连接窗口中，右键单击一个无法识别的网络槽 Mellanox 适配器并选择属性。  
  
    ![选择 InfiniBand 网络](media/network-connections.png "选择 InfiniBand 网络")  
  
2.  在属性窗口  
  
    1.  在常规选项卡上，将 IP 地址设置验证为 TeamIB1 ping 测试中可用的 IP 地址。 查看本文中使用的示例值，您可以输入 172.16.14.254。  
  
    2.  设置为子网掩码为 TeamIB1 记下的子网掩码。  
  
    3.  将首选 DNS 服务器设置为 TeamIB1 appliance_domain * 从前面记下的 IP 地址-AD01 节点。  
  
    4.  将备用 DNS 服务器设置为 TeamIB1 appliance_domain * 从前面记下的 IP 地址-AD02 节点。  
  
        ![InfiniBand 1 个网络适配器属性](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  单击确定以应用更改。  
  
### <a name="to-configure-the-second-network-adapter"></a>若要配置的第二个网络适配器  
  
1.  如果只有一个网络适配器，请跳过此部分。  
  
2.  在网络连接窗口中，右键单击第二个未识别的网络段上为 Mellanox 适配器并选择属性。  
  
    ![选择 InfiniBand 网络](media/network-connections.png "选择 InfiniBand 网络")  
  
3.  在属性窗口  
  
    1.  在常规选项卡上，将 IP 地址设置验证为 ping 测试 TeamIB2 的属性中可用的 IP 地址。 查看本文中使用的示例值，您可以输入 172.16.18.254。  
  
    2.  设置为子网掩码为 TeamIB2 记下的子网掩码。  
  
    3.  将首选 DNS 服务器设置为前面记从 appliance_domain * TeamIB2 的 IP 地址-AD01 节点。  
  
    4.  将备用 DNS 服务器设置为前面记从 appliance_domain * TeamIB2 的 IP 地址-AD02 节点。  
  
        > [!NOTE]  
        > 如果只有一个网络适配器，配置首选和备用 DNS 服务器作为首选和备用 DNS 服务器分别使用设备 AD01 TeamIB1 和设备 AD02 TeamIB1 或使用设备 AD01 TeamIB2 和设备 AD02 TeamIB2 为首选和备用的 DNS 服务器，具体取决于 AD 虚拟机已故障转移。  
  
        ![InfiniBand 1 个网络适配器属性](media/network-ib1-properties.png "InfiniBand 1 个网络适配器属性")  
  
    5.  单击确定以应用更改。  
  
### <a name="to-configure-the-dns-suffix"></a>若要配置的 DNS 后缀  
  
1.  在网络连接窗口中，右键单击其中一个网络插槽 Mellanox 适配器并选择属性。  
  
2.  单击高级...按钮。  
  
3.  在高级 TCP/IP 设置窗口中，如果追加这些 DNS 后缀 （按顺序） 选项并不灰显，复选框称作附加这些 DNS 后缀 （按顺序）:，选择设备域后缀，然后单击添加...设备域后缀是 `appliance_domain.local`  
  
4.  如果附加这些 DNS 后缀 （按顺序）： 选项灰显，您可以通过修改注册表项 HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient APS 域添加到此服务器。  
  
    ![TCP/IP 设置](media/network-tcpip.png "TCP/IP 设置")  
  
5.  对于速度更快的地址解析，我们建议将设备后缀移到列表的顶部。  
  
6.  单击“确定”。  
  
7.  现在，你可以使用连接到设备 Infiniband 网络`PDW_region-SQLCTL01.appliance_domain.local`，或只需`appliance_domain-SQLCTL01`。 如果你使用的完整名称和 DNS 后缀连接可能会更快地建立的连接。  
  
    一台设备的示例与 MyPDW PDW 区域命名 MyAPS:  
  
    -   MyPDW-SQLCTL01.MyAPS.local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>请参阅  
[获取和配置加载服务器 ](acquire-and-configure-loading-server.md)  
  
