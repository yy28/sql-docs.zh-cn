---
title: 配置故障转移群集实例存储 iSCSI-Linux 上的 SQL Server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 9a64460b2d04f1d6957a181657af7255d64cc829
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705069"
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>配置故障转移群集实例-iSCSI-Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上配置 iSCSI 存储为故障转移群集实例 (FCI)。 

## <a name="configure-iscsi"></a>配置 iSCSI 
iSCSI 使用网络来提供从服务器到服务器的已知目标磁盘。 连接到 iSCSI 目标服务器需要配置 iSCSI 发起程序。 在目标上的磁盘提供显式权限，以便能够对其进行访问的发起程序可以这样做。 高可用性和可靠性，应为目标本身。

### <a name="important-iscsi-target-information"></a>重要的 iSCSI 目标信息
虽然本部分将介绍如何配置 iSCSI 目标，因为它是特定于你将使用的源的类型，请确保配置将由群集节点的磁盘的安全性。  

如果使用基于 Linux 的 iSCSI 目标，目标应永远不会配置任何 FCI 节点上。 有关性能和可用性，iSCSI 网络应独立于所使用的源服务器和客户端服务器上的常规网络流量。 用于 iSCSI 的网络应该速度很快。 请记住该网络不使用某些处理器带宽，因此如果使用常规服务器相应地规划。
要确保的最重要一点是在目标上完成是将创建的磁盘分配适当的权限，以便仅在 FCI 中加入这些服务器有权访问它们。 从 Microsoft iSCSI 目标其中 linuxnodes1 是创建，名称，在这种情况下，节点的 IP 地址分配，以便向其显示 NewFCIDisk1.vhdx 下面显示了一个示例。

![Initiator][1]

### <a name="instructions"></a>Instructions

本部分将介绍如何将充当 FCI 节点的服务器上配置 iSCSI 发起程序。 在 RHEL 和 Ubuntu，说明应适用。

ISCSI 发起程序的受支持的分发版的详细信息，请参阅以下链接：
- [Red Hat](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](https://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  在 FCI 配置中选择一个将加入的服务器。 并不重要哪一个。 iSCSI 应为在专用网络中，因此配置 iSCSI 以便识别和使用该网络。 运行`sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new`其中`<iSCSIIfaceName>`是网络的唯一或友好名称。 下面的示例使用`iSCSINIC`:
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  编辑`/var/lib/iscsi/ifaces/iSCSIIfaceName`。 请确保它已完全填写以下值：

    - iface.net_ifacename 并在操作系统中所示的网络卡的名称。
    - iface.hwaddress 是将创建以下此接口的唯一名称的 MAC 地址。
    - iface.ipaddress
    - iface.subnet_Mask 

    请参阅以下示例：

    ![iSCSITargetSettings][2]

3.  发现 iSCSI 目标。

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName > 是在网络中，唯一/友好名称\<TargetIPAddress > 是 iSCSI 目标的 IP 地址和\<TargetPort > 是 iSCSI 目标的端口。 

    ![iSCSITargetResults][3]

 
4.  登录到目标

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName > 是网络的唯一/友好名称和\<TargetIPAddress > 是 iSCSI 目标的 IP 地址。

    ![iSCSITargetLogin][4]

5.  检查连接到 iSCSI 目标。

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  检查 iSCSI 附加磁盘

    ```bash
    sudo grep "Attached SCSI" /var/log/messages
    ```
    ![30-iSCSIattachedDisks][7]

7.  在 iSCSI 磁盘上创建物理卷。

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<devicename > 是上一步中的设备的名称。 

 
8.  在 iSCSI 磁盘上创建卷组。 分配给单个卷组的磁盘被视为池或集合。 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName > 是卷组的名称和\<devicename > 是从步骤 6 设备的名称。 
 
9.  创建并验证逻辑磁盘卷。

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<大小 > 是要进行创建，卷的大小，可以使用 G （千兆字节为单位） 和 T （兆兆字节） 等，指定\<LogicalVolumeName > 是逻辑卷的名称和\<VolumeGroupName > 是从卷组的名称上一步。 

    下面的示例创建的 25 GB 卷。
 
    ![Create25GBVol][10]

10. 执行`sudo lvs`若要查看已创建 LVM。
 
11. 格式化逻辑卷与受支持的文件系统。 对于 EXT4，请使用下面的示例：

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName > 是上一步中的卷组的名称。 \<LogicalVolumeName > 是在上一步中的逻辑卷的名称。  

12. 对于系统数据库或存储在默认数据位置的任何内容，请执行以下步骤。 否则，跳到步骤 13。

   *    请确保 SQL Server 已停止正在努力在服务器上。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    开关完全是超级用户。 如果成功，将不会收到任何确认。

    ```bash
    sudo -i
    ```

   *    要使用 mssql 用户的开关。 如果成功，将不会收到任何确认。

    ```bash
    su mssql
    ```

   *    创建一个临时目录来存储 SQL Server 数据和日志文件。 如果成功，将不会收到任何确认。

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > 是文件夹的名称。 下面的示例创建一个名为 /var/opt/mssql/TempDir 文件夹。

    ```bash
    mkdir /var/opt/mssql/TempDir
    ```
    
   *    将 SQL Server 数据和日志文件复制到临时目录。 如果成功，将不会收到任何确认。

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > 是上一步中的文件夹的名称。
    
   *    验证文件在目录中。

    ```bash
    ls \<TempDir>
    ```
    \<TempDir > 是从步骤 d 文件夹的名称。

   *    从现有的 SQL Server 数据目录中删除的文件。 如果成功，将不会收到任何确认。

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   *    验证已删除的文件。 下图显示了从 c 到 h 的整个序列示例。

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45-CopyMove][8]
 
   *    类型`exit`若要切换回根用户。

   *    安装 SQL Server 数据文件夹中的 iSCSI 逻辑卷。 如果成功，将不会收到任何确认。

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName > 是卷组的名称和\<LogicalVolumeName > 是已创建的逻辑卷的名称。 下面的示例语法匹配的卷组和前一命令的逻辑卷。

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    更改为 mssql 装载的所有者。 如果成功，将不会收到任何确认。

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    装载的组的所有权更改为 mssql。 如果成功，将不会收到任何确认。

    ```bash
    chgrp mssql /var/opt/mssql/data
    ``` 

   *    切换到 mssql 用户。 如果成功，将不会收到任何确认。

    ```bash
    su mssql
    ``` 

   *    将文件从临时目录 /var/opt/mssql/data 复制。 如果成功，将不会收到任何确认。

    ```bash
    cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
    ``` 

   *    验证文件存在。

    ```bash
    ls /var/opt/mssql/data
    ``` 
 
   *    输入`exit`不为 mssql。
    
   *    输入`exit`使其不作为根。

   *    启动 SQL Server。 如果已正确复制所有内容和应用的安全设置是否正确，SQL Server 应显示为已启动。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    停止 SQL Server，并验证它关闭的情况下。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. 为系统数据库，例如，用户数据库或备份以外的内容，请执行以下步骤。 如果只使用了默认位置，请跳至步骤 14。

   *    切换到是超级用户。 如果成功，将不会收到任何确认。

    ```bash
    sudo -i
    ```

   *    创建 SQL Server 将使用的文件夹。 

    ```bash
    mkdir <FolderName>
    ```

    \<文件夹名 > 是文件夹的名称。 文件夹的完整路径需要指定如果不在正确的位置。 下面的示例创建一个名为 /var/opt/mssql/userdata 文件夹。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    装载的文件夹中的上一步中创建 iSCSI 逻辑卷。 如果成功，将不会收到任何确认。
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > 是卷组的名称\<LogicalVolumeName > 是已创建的逻辑卷的名称和\<文件夹名 > 是文件夹的名称。 示例语法如下所示。

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    更改到 mssql 创建的文件夹的所有权。 如果成功，将不会收到任何确认。

    ```bash
    chown mssql <FolderName>
    ```

    \<文件夹名 > 是已创建的文件夹的名称。 以下是一个示例。

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    更改到 mssql 创建的文件夹的组。 如果成功，将不会收到任何确认。

    ```bash
    chown mssql <FolderName>
    ```

    \<文件夹名 > 是已创建的文件夹的名称。 以下是一个示例。

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    类型`exit`不再是超级用户身份。

   *    若要测试，请在该文件夹中创建数据库。 如下所示的示例使用 sqlcmd 创建数据库，将上下文切换到它，验证文件存在于 OS 级别，然后删除该临时位置。 可以使用 SSMS。
  
    ![50-ExampleCreateSSMS][9]

   *    卸载共享 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > 是卷组的名称\<LogicalVolumeName > 是已创建的逻辑卷的名称和\<文件夹名 > 是文件夹的名称。 示例语法如下所示。

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. 配置服务器，以便该唯一 Pacemaker 可以激活的卷组。

    ```bash
    sudo lvmconf --enable-halvm --services -startstopservices
    ```
 
15. 生成服务器上的卷组的列表。 列出不的任何内容的 iSCSI 磁盘可供系统，如对 OS 磁盘。

    ```bash
    sudo vgs
    ```

16. 修改文件 /etc/lvm/lvm.conf 的激活配置节。 配置以下行：

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker > 是输出中将不能由 FCI 的步骤 20 个卷组的列表。 将逗号分隔每个用引号引起来的独立。 以下是一个示例。

    ![55-ListOfVGs][11]
 
 
17. Linux 启动时，它将安装文件系统。 若要确保仅 Pacemaker 可以装载的 iSCSI 磁盘，请重新生成的根文件系统映像。 

    运行以下命令，这可能需要一些时间才能完成。 如果成功，将返回收到任何消息。

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. 重新启动服务器。

19. 在将参与 FCI 的另一台服务器，执行步骤 1-6。 这将为 SQL Server 提供 iSCSI 目标。 
 
20. 生成服务器上的卷组的列表。 它应显示前面创建的卷组。 

    ```bash
    sudo vgs
    ``` 
23. 启动 SQL Server，并验证此服务器上启动它。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. 停止 SQL Server，并验证它已关闭。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. 重复步骤 1-6 将参与 FCI 的任何其他服务器上。

你现已准备好配置 FCI。

|Distribution |主题 
|----- |-----
|**附带 HA 加载项的 Red Hat Enterprise Linux** |[配置](sql-server-linux-shared-disk-cluster-configure.md)<br/>[操作](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**附带 HA 加载项的 SUSE Linux Enterprise Server** |[配置](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>后续步骤

[配置故障转移群集实例-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/05-initiator.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/10-iscsiTargetSettings.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/15-iSCSITargetResults.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/20-iSCSITargetLogin.png
[5]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/25-iSCSIVerify.png
[6]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/7-setiscsinetwork.png
[7]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/30-iSCSIattachedDisks.png
[8]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/45-CopyMove.png
[9]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/50-ExampleCreateSSMS.png
[10]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/40-Create25GBVol.png
[11]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/55-ListOfVGs.png
