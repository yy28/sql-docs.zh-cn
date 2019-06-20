---
title: 获取和配置备份服务器-并行数据仓库 |Microsoft Docs
description: 本文介绍如何将非设备 Windows 系统配置为备份服务器用于与 Analytics Platform System (APS) 和并行数据仓库 (PDW) 中的备份和还原功能一起使用。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: cba345eb7a5aec9ef857819a1f0499266649f6e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63040823"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>获取和并行数据仓库配置备份服务器
本文介绍如何将非设备 Windows 系统配置为备份服务器用于与 Analytics Platform System (APS) 和并行数据仓库 (PDW) 中的备份和还原功能一起使用。  
  
  
## <a name="Basics"></a>备份服务器基础知识  
备份服务器：  
  
-   提供并由 IT 团队管理。  
  
-   不需要任何特定于 PDW 的软件或工具。 PDW 不会安装到备份服务器上的任何软件。  
  
-   位于您自己的非设备机架，且不能放置在 APS 设备。  
  
-   可以连接到设备 InfiniBand 网络。 可以通过 InfiniBand 或以太网; 执行备份出于性能原因，建议 InfiniBand。  
  
-   是在您自己客户域中，不是在设备域。 客户域的设备域之间没有信任关系。  
  
-   托管备份文件共享，这是使用服务器消息块 (SMB) 应用程序级别网络协议的 Windows 文件共享。 备份文件共享权限向 Windows 域用户 （通常这是专用的备份用户） 提供的功能来执行备份和还原共享上的操作。 Windows 域用户的用户名和密码凭据存储在 PDW 中，以便 PDW 可以执行备份和还原备份文件共享上的操作。  
  
## <a name="Step1"></a>步骤 1:确定容量要求  
备份服务器的系统要求几乎完全取决于自己的工作负荷。 在购买或预配备份服务器之前，您需要找出你的容量要求。 备份服务器不必是专用的备份，只要它将处理工作负荷的性能和存储要求。 此外可以具有多个备份服务器备份和还原到多个服务器之一的每个数据库。  
  
使用[备份服务器容量规划工作表](backup-capacity-planning-worksheet.md)以帮助确定容量要求。  
  
## <a name="Step2"></a>步骤 2:获取备份服务器  
现在，更好地了解你的容量要求，您可以计划的服务器和网络将需要购买或预配的组件。 将下面的要求列表合并到你购买的计划，然后购买你的服务器或预配的现有服务器。  
  
### <a name="software-requirements"></a>软件要求  
使用 Windows 文件共享 (SMB) 协议的任何文件服务器。  
  
我们建议 Windows Server 2012 或更高版本以便：  
  
-   SMB 上获取文件预先分配的性能优势。  
  
-   为备份操作使用即时文件初始化 (IFI)。 你的 IT 团队管理备份的服务器上此设置。 PDW 配置管理器 (dwconfig.exe) 不设置，也不控制 IFI 备份服务器上。 以前版本的 Windows 没有 IFI，但仍可用作备份服务器。  
  
### <a name="networking-requirements"></a>网络要求  
尽管没有要求，无限带宽是备份服务器的建议的连接类型。 准备加载服务器连接到设备 InfiniBand 网络：  
  
1.  计划安装机架服务器关闭足够到设备，以便可以将其连接到 InfiniBand 切换的设备。 有关 InfiniBand 从 Mellanox 技术的详细信息，请参阅白皮书[简介 InfiniBand](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)。  
  
2.  购买 Mellanox ConnectX 3 FDR InfiniBand 单或双端口的网络适配器。 我们建议在数据传输过程中购买的容错能力的两个端口的网络适配器。 为实现高可用性需要两个端口网络适配器。  
  
3.  购买 2 个 FDR InfiniBand 电缆双端口卡片或为单个端口卡 1 FDR InfiniBand 网络。 FDR InfiniBand 电缆将连接到设备 InfiniBand 网络加载服务器。 电缆长度取决于加载服务器和设备 InfiniBand 交换机之间的距离根据您的环境。  
  
## <a name="Step3"></a>步骤 3:将服务器连接到 InfiniBand 网络  
使用以下步骤将加载服务器连接到 InfiniBand 网络。 如果服务器不使用 InfiniBand 网络，请跳过此步骤。  
  
1.  机架服务器得足够近到设备，以便可以将其连接到设备 InfiniBand 网络。  
  
2.  将 InfiniBand Mellanox ConnectX 3 FDR InfiniBand 网络适配器安装到加载服务器。  
  
3.  使用以 FDR 电缆 InfiniBand 网络适配器连接到第一个设备机架中的两个 InfiniBand 开关之一。  
  
4.  安装和配置 InfiniBand 网络适配器的相应 Windows 驱动程序。  
  
    -   Windows 的 InfiniBand 驱动程序开发的 OpenFabrics 联盟的 InfiniBand 供应商。  使用 InfiniBand 网络适配器中，可能已分发的正确驱动程序。 如果没有，可以从 www.openfabrics.org 下载驱动程序。  
  
5.  配置网络适配器的 InfiniBand 和 DNS 设置。 有关配置说明，请参阅[配置无线带宽技术网络适配器](configure-infiniband-network-adapters.md)。  
  
## <a name="Step4"></a>步骤 4:配置备份的文件共享  
PDW 将通过 UNC 文件共享中访问备份的服务器。 若要设置的文件共享：  
  
1.  用于存储备份的备份服务器上创建一个文件夹。  
  
2.  创建文件共享，调用对备份文件夹的备份共享。  
  
3.  指定或你想要用于执行备份和还原的目的在客户域中创建一个 Windows 域帐户。 出于安全原因，最好使用专用的帐户作为备份的用户。  
  
4.  将添加到备份权限共享，以便仅受信任的帐户和域备份帐户可以访问，读取和写入到共享位置。  
  
5.  将备份的域帐户凭据添加到 PDW。  
  
    例如：  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    有关详细信息，请参阅这些存储的过程：  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>步骤 5:开始备份你的数据  
现在您就可以开始备份到备份服务器数据。  
  
若要备份的数据，请使用查询客户端连接到 SQL Server PDW，然后提交备份或还原数据库命令。 使用磁盘 = 子句来指定备份服务器和备份位置。  
  
> [!IMPORTANT]  
> 请记住使用备份服务器的 InfiniBand IP 地址。 否则，数据将复制而不是 InfiniBand 的以太网。  
  
例如：  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
有关详细信息，请参阅： 
  
-   [备份数据库](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>安全通知  
备份服务器未加入到该设备的专用域中。 在您自己的网络，并且没有自己的域和专用设备域之间没有信任关系。  
  
由于 PDW 备份不存储在设备上，你的 IT 团队负责管理备份安全的所有方面。 例如，这包括管理备份数据、 用于存储备份，服务器的安全和备份服务器连接到 APS 设备的网络基础结构安全的安全性。  
  
### <a name="manage-network-credentials"></a>管理网络凭据  
  
对备份目录的网络访问权限基于标准 Windows 文件共享安全。 在执行之前备份，需要创建或指定将用于向备份目录进行 PDW 身份验证的 Windows 帐户。 此 Windows 帐户必须有权访问、创建和写入备份目录。  
  
> [!IMPORTANT]  
> 若要降低数据的安全风险，建议指定一个 Windows 帐户专门用于执行备份和还原操作。 仅允许此帐户访问备份位置，不要授予对其他位置的访问权限。  
  
若要在 PDW 中存储的用户名和密码，请使用[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)存储过程。 PDW 使用 Windows 凭据管理器来存储和加密用户名和密码在控制节点和计算节点。 不使用 BACKUP DATABASE 命令备份凭据。  
  
若要从 PDW 删除网络凭据，请使用[sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)存储过程。  
  
若要列出所有 SQL Server PDW 中存储的网络凭据，请使用[sys.dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)动态管理视图。  
  
### <a name="secure-communications"></a>安全通信  
  
加载服务器上的操作可以使用来自受信任的内部网络之外的请求数据的 UNC 路径。 在网络上或能够影响名称解析攻击者可以截获或修改数据发送到 PDW。 这带来篡改和信息泄露的风险。 若要帮助缓解篡改的风险：

- 需要在连接上签名。 
- 在加载服务器上，安全设置 \ 本地策略 \ 安全选项中设置以下组策略选项：Microsoft 网络客户端：数字签名通信 （始终）：已启用。  
  
## <a name="see-also"></a>请参阅  
[备份和还原](backup-and-restore-overview.md)  
  
