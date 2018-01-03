---
title: "获取和为 AP PDW 配置备份服务器"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "将非设备 Windows 系统配置为备份服务器用于备份和还原分析平台系统 (AP) 和 SQL Server 并行数据仓库 (PDW) 中的功能。"
ms.date: 10/20/2016
ms.topic: article
caps.latest.revision: "20"
ms.assetid: f8b769fe-c864-4d65-abcb-a9a287061702
ms.openlocfilehash: 760537abd7e3227cc2245c429d0a0c13f7609f8b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="acquire-and-configure-a-backup-server"></a>获取和配置备份服务器
本主题介绍如何将非设备 Windows 系统配置为与备份和还原功能在分析平台系统 (AP) 一起使用的备份服务器和 SQL Server 并行数据仓库 (PDW)。  
  
  
## <a name="Basics"></a>备份服务器基础知识  
备份服务器：  
  
-   提供和由你自己的 IT 团队。  
  
-   不需要任何 PDW 特定软件或工具。 PDW 不安装任何软件到备份服务器。  
  
-   位于你自己的非设备机架，并且不能放置在 AP 设备。  
  
-   可以连接到设备 InfiniBand 网络。 可以通过 InfiniBand 或以太网; 执行备份出于性能原因，建议 InfiniBand。  
  
-   是在你自己客户域中，不是在设备域。 客户域和设备的域之间没有信任关系。  
  
-   托管备份文件共享，即使用服务器消息块 (SMB) 应用程序级别网络协议的 Windows 文件共享。 备份文件共享权限授予 Windows 域用户 （通常这是专用的备份用户） 执行备份和还原在共享上的操作的能力。 Windows 域用户的用户名和密码凭据都存储在 PDW 中，以便 PDW 可以执行备份和还原备份文件共享上的操作。  
  
## <a name="Step1"></a>步骤 1： 确定容量需求  
备份服务器的系统要求几乎完全取决于你自己的工作负荷。 在购买或预配备份服务器之前，您需要找出你的容量要求。 备份服务器不必是专用的备份，只要它将处理你的工作负荷的性能和存储要求。 你还可以以备份和还原到多个服务器之一的每个数据库的多个备份服务器。  
  
使用[备份服务器容量规划工作表](backup-capacity-planning-worksheet.md)以帮助确定你的容量要求。  
  
## <a name="Step2"></a>步骤 2： 获取备份服务器  
现在，你更好地了解你的容量要求，你可以计划的服务器和网络将需要购买，也可以设置的组件。 将下面列出的要求合并到你购买的计划，然后购买你的服务器或配置现有服务器。  
  
### <a name="software-requirements"></a>软件要求  
使用 Windows 文件共享 (SMB) 协议的任何文件服务器。  
  
我们建议 Windows Server 2012 或更以便：  
  
-   SMB 上获取文件预分配的性能优势。  
  
-   为备份操作使用即时文件初始化 (IFI)。 你的 IT 团队管理备份服务器上的此设置。 PDW Configuration Manager (dwconfig.exe) 不设置，也不控制 IFI 备份服务器上。 以前版本的 Windows 不具有 IFI，但仍可用作备份服务器。  
  
### <a name="networking-requirements"></a>网络要求  
尽管没有要求，无限带宽是备份服务器的建议的连接类型。 若要准备将加载服务器连接到的设备 InfiniBand 网络：  
  
1.  计划机架服务器关闭足够到设备，以便你可以将其连接到设备 InfiniBand 切换。 有关 InfiniBand 和 Mellanox 技术的详细信息，请参阅白皮书，[简介 InfiniBand](http://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)。  
  
2.  购买 Mellanox connectx-3 FDR InfiniBand 单或双端口的网络适配器。 我们建议在数据传输过程购买容错功能的两个端口的网络适配器。 为实现高可用性需要两个端口的网络适配器。  
  
3.  购买 2 FDR InfiniBand 条电缆，用于双端口卡或为单个端口卡 1 FDR InfiniBand 电缆。 FDR InfiniBand 电缆将连接到设备 InfiniBand 网络加载服务器。 电缆长度取决于在加载服务器和设备 InfiniBand 交换机之间的距离根据你的环境。  
  
## <a name="Step3"></a>步骤 3： 将服务器连接到的 InfiniBand 网络  
使用这些步骤将加载服务器连接到的 InfiniBand 网络。 如果服务器未使用 InfiniBand 网络，跳过此步骤。  
  
1.  机架服务器足够近到设备，以便你可以将其连接到的设备 InfiniBand 网络。  
  
2.  将 InfiniBand Mellanox connectx-3 FDR InfiniBand 网络适配器安装到加载服务器。  
  
3.  使用 FDR 电缆 InfiniBand 网络适配器连接到第一个设备机架中的两个 InfiniBand 开关之一。  
  
4.  安装和配置适当 Windows InfiniBand 网络适配器驱动程序。  
  
    -   适用于 Windows InfiniBand 驱动程序是通过 OpenFabrics 联盟，InfiniBand 供应商行业联合会开发的。  正确的驱动程序可能已与你 InfiniBand 网络适配器中分发。 如果没有，可以从 www.openfabrics.org 下载驱动程序。  
  
5.  配置网络适配器的 InfiniBand 和 DNS 设置。 有关配置说明，请参阅[配置无线带宽技术网络适配器](configure-infiniband-network-adapters.md)。  
  
## <a name="Step4"></a>步骤 4： 配置备份文件共享  
PDW 将通过一个 UNC 文件共享访问备份服务器。 若要将文件共享设置：  
  
1.  在存储备份的备份服务器上创建一个文件夹。  
  
2.  创建文件共享，备份文件夹将为调用的备份共享。  
  
3.  指定或在你想要使用用于执行的备份和还原目的的客户域中创建一个 Windows 域帐户。 出于安全原因，最好的专用的帐户用作备份的用户。  
  
4.  添加到备份的权限共享读取，因此，只有受信任的帐户和域备份帐户可以访问，并将写入的共享位置。  
  
5.  将备份的域帐户凭据添加到 PDW。  
  
    例如：  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    有关详细信息，请参阅这些存储的过程：  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>步骤 5： 开始备份你的数据  
现在你就可以开始备份到备份服务器数据。  
  
若要备份的数据，请使用查询客户端连接到 SQL Server PDW，然后提交备份或还原数据库的命令。 使用磁盘 = 子句，以指定备份服务器和备份位置。  
  
> [!IMPORTANT]  
> 请记得使用备份的服务器的 InfiniBand IP 地址。 否则，将通过以太网，而不是 InfiniBand 复制数据。  
  
例如：  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
有关详细信息，请参阅： 
  
-   [备份数据库](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [还原数据库](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>安全声明  
备份服务器未加入到设备的专用域中。 在您自己的网络，并且没有自己的域和专用设备域之间没有信任关系。  
  
由于 PDW 备份不存储在设备上，你的 IT 团队负责管理备份安全性的各个方面。 例如，这包括管理备份的数据、 用于存储备份，服务器的安全性和连接到 AP 设备的备份的服务器的网络基础结构的安全性的安全性。  
  
### <a name="manage-network-credentials"></a>管理网络凭据  
  
对备份目录的网络访问权限基于标准 Windows 文件共享安全。 在执行之前备份，需要创建或指定将用于向备份目录进行 PDW 身份验证的 Windows 帐户。 此 windows 帐户必须有权访问、 创建和写入备份目录。  
  
> [!IMPORTANT]  
> 若要减少与你的数据的安全风险，我们建议您指定一个 Windows 帐户专门用于执行备份和还原操作。 允许此帐户具有对备份的位置和其他地方的权限。  
  
若要在 PDW 中存储的用户名和密码，使用[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)存储过程。 PDW 使用 Windows 凭据管理器来存储和加密用户名和密码的控件节点和计算节点。 凭据不会备份使用 BACKUP DATABASE 命令所造成。  
  
若要从 PDW 中删除网络凭据，使用[sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)存储过程。  
  
若要列出所有 SQL Server PDW 中存储的网络凭据，请使用[sys.dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)动态管理视图。  
  
### <a name="secure-communications"></a>安全通信  
  
加载服务器上的操作可以使用来自受信任的内部网络外部的请求数据的 UNC 路径。 攻击者在网络上还是能够影响名称解析可以截获或修改数据发送到 PDW。 这存在篡改和信息泄露风险。 若要帮助缓解被篡改的风险：

- 要求签名连接上。 
- 在加载服务器上，在安全设置 \ 本地策略 \ 安全选项中设置以下的组策略选项： Microsoft 网络客户端： 数字签名通信 （始终）： 启用。  
  
## <a name="see-also"></a>另请参阅  
[备份和还原](backup-and-restore-overview.md)  
  
