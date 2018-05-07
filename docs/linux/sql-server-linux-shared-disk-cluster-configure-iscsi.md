---
title: 配置故障转移群集实例存储 iSCSI-在 Linux 上的 SQL Server |Microsoft 文档
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 514d19e4358b536109c76112115bac380f390bce
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>配置故障转移群集实例-iSCSI-在 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文章介绍了如何在 Linux 上配置的故障转移群集实例 (FCI) 的 iSCSI 存储。 

## <a name="configure-iscsi"></a>配置 iSCSI 
iSCSI 使用网络来提供从服务器到服务器称为目标的磁盘。 连接到 iSCSI 目标服务器需要配置 iSCSI 发起程序。 在目标上的磁盘会获得显式权限，以便应该能够访问它们的发起者可以执行此操作。 Target 本身应该是高可用性和可靠性。

### <a name="important-iscsi-target-information"></a>重要的 iSCSI 目标信息
虽然本部分将不介绍如何配置 iSCSI 目标，因为它是特定于你将使用的源的类型，将确保配置将由群集节点的磁盘的安全性。  

如果使用基于 Linux 的 iSCSI 目标，则不应在任何 FCI 节点上配置目标。 有关性能和可用性，iSCSI 网络，应将与所使用的正则源服务器和客户端服务器上的网络流量分开。 用于 iSCSI 的网络应快速。 请记住该网络不使用某些处理器的带宽，因此如果使用常规服务器相应地进行规划。
最重要的事情，以确保在目标上完成的是，将磁盘创建分配适当的权限，以便仅在 FCI 参与这些服务器有权访问它们。 从 Microsoft iSCSI 目标其中 linuxnodes1 创建的名称，并且在这种情况下，节点的 IP 地址分配以便 NewFCIDisk1.vhdx 显示给他们的示例所示。

![Initiator][1]

### <a name="instructions"></a>Instructions

本部分将介绍如何在将充当 FCI 节点的服务器上配置 iSCSI 发起程序。 作为在 RHEL 和 Ubuntu 上，应运行说明。

有关受支持的分发的 iSCSI 发起程序的详细信息，请参阅以下链接：
- [Red Hat](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](http://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  在 FCI 配置中选择一个将加入的服务器。 它并不重要哪一个。 iSCSI 应为在专用网络上，因此配置 iSCSI 来识别并使用该网络。 运行`sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new`其中`<iSCSIIfaceName>`是网络的唯一或友好名称。 下面的示例使用`iSCSINIC`:
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  编辑`/var/lib/iscsi/ifaces/iSCSIIfaceName`。 请确保它有完全填写以下值：

    - 在操作系统中所示，iface.net_ifacename 是网络卡的名称。
    - iface.hwaddress 是将为此接口下面创建的唯一名称的 MAC 地址。
    - iface.ipaddress
    - iface.subnet_Mask 

    请参阅以下示例：

    ![iSCSITargetSettings][2]

3.  查找 iSCSI 目标。

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName > 是网络的唯一/友好名称\<TargetIPAddress > 是 iSCSI 目标的 IP 地址和\<TargetPort > 是的 iSCSI 目标端口。 

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
    sudo grep “Attached SCSI” /var/log/messages
    ```
    ![30 iSCSIattachedDisks][7]

7.  在 iSCSI 磁盘上创建物理卷。

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<devicename > 是上一步中设备的名称。 

 
8.  在 iSCSI 磁盘上创建卷组。 分配给单个卷组的磁盘被看作是池或集合。 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName > 是的卷组的名称和\<devicename > 是从步骤 6 设备的名称。 
 
9.  创建并验证磁盘的逻辑卷。

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<大小 > 是要创建的卷的大小，并且可以指定与 G （千兆字节为单位）、 T （兆兆字节） 等\<LogicalVolumeName > 是的逻辑卷的名称和\<VolumeGroupName > 是从卷组的名称上一步。 

    下面的示例创建了 25 GB 卷。
 
    ![Create25GBVol][10]

10. 执行`sudo lvs`若要查看已创建 LVM。
 
11. 具有受支持的文件系统的逻辑卷进行格式化。 对于 EXT4，请使用下面的示例：

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName > 是前一步骤中的卷组的名称。 \<LogicalVolumeName > 是上一步中的逻辑卷的名称。  

12. 对于系统数据库或存储在默认数据位置的任何内容，请按照下列步骤。 否则，请跳到步骤 13。

   *    确保 SQL Server 已停止您正在使用的服务器上。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    完全要超级用户身份的开关。 如果成功，将不会收到任何确认。

    ```bash
    sudo -i
    ```

   *    要 mssql 用户的开关。 如果成功，将不会收到任何确认。

    ```bash
    su mssql
    ```

   *    创建一个临时的目录来存储 SQL Server 数据和日志文件。 如果成功，将不会收到任何确认。

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

    \<TempDir > 是前一步骤中的文件夹的名称。
    
   *    验证文件在目录中。

    ```bash
    ls \<TempDir>
    ```
    \<TempDir > 是来自步骤 d 的文件夹的名称。

   *    从现有的 SQL Server 数据目录删除这些文件。 如果成功，将不会收到任何确认。

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   *    验证文件已被删除。 下图显示从 c 到 h 的整个序列示例。

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45-CopyMove][8]
 
   *    类型`exit`若要切换回根用户。

   *    安装 SQL Server 数据文件夹中的 iSCSI 逻辑卷。 如果成功，将不会收到任何确认。

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName > 是的卷组的名称和\<LogicalVolumeName > 是创建的逻辑卷的名称。 下面的示例语法与卷组和前一个命令中的逻辑卷匹配。

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    将装入的所有者更改为 mssql。 如果成功，将不会收到任何确认。

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    将装入的组的所有权更改为 mssql。 如果成功，将不会收到任何确认。

    ```bash
    chgrp mssql /var/opt/mssql/data
    ``` 

   *    切换到 mssql 用户。 如果成功，将不会收到任何确认。

    ```bash
    su mssql
    ``` 

   *    从临时目录 /var/opt/mssql/data 文件复制。 如果成功，将不会收到任何确认。

    ```bash
    cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
    ``` 

   *    验证文件存在。

    ```bash
    ls /var/opt/mssql/data
    ``` 
 
   *    输入`exit`不 mssql。
    
   *    输入`exit`不会是根。

   *    启动 SQL Server。 如果正确复制的所有内容和应用安全设置是否正确，SQL Server 应显示为已启动。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    停止 SQL Server，并验证它关闭。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. 对于操作以外系统数据库，如用户数据库或备份，请按照这些步骤。 如果仅使用默认位置，请跳至步骤 14。

   *    为超级用户身份的开关。 如果成功，将不会收到任何确认。

    ```bash
    sudo -i
    ```

   *    创建 SQL Server 将使用一个文件夹。 

    ```bash
    mkdir <FolderName>
    ```

    \<文件夹名称 > 是文件夹的名称。 该文件夹的完整路径，需要指定如果不在正确的位置。 下面的示例创建一个名为 /var/opt/mssql/userdata 文件夹。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    将 iSCSI 逻辑卷上一步中创建的文件夹中装入。 如果成功，将不会收到任何确认。
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > 是的卷组中，名称\<LogicalVolumeName > 是已创建的逻辑卷的名称和\<FolderName > 是文件夹的名称。 示例语法如下所示。

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    更改到 mssql 创建的文件夹的所有权。 如果成功，将不会收到任何确认。

    ```bash
    chown mssql <FolderName>
    ```

    \<文件夹名称 > 是已创建的文件夹的名称。 以下是一个示例。

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    更改到 mssql 创建的文件夹的组。 如果成功，将不会收到任何确认。

    ```bash
    chown mssql <FolderName>
    ```

    \<文件夹名称 > 是已创建的文件夹的名称。 以下是一个示例。

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    类型`exit`不再为超级用户。

   *    若要测试，请在该文件夹中创建数据库。 下面所示的示例使用 sqlcmd 创建数据库，将上下文切换到它，验证文件中的操作系统级别中，存在，然后删除的临时位置。 你可以使用 SSMS。
  
    ![50 ExampleCreateSSMS][9]

   *    卸载共享 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > 是的卷组中，名称\<LogicalVolumeName > 是已创建的逻辑卷的名称和\<FolderName > 是文件夹的名称。 示例语法如下所示。

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. 配置服务器，以便该唯一 Pacemaker 可以激活的卷组。

    ```bash
    sudo lvmconf --enable-halvm --services –startstopservices
    ```
 
15. 生成服务器上的卷组的列表。 以外的任何列出的 iSCSI 磁盘用于系统，如操作系统磁盘。

    ```bash
    sudo vgs
    ```

16. 修改文件 /etc/lvm/lvm.conf 的激活配置节。 配置以下行：

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker > 是的输出将不能由 FCI 的步骤 20 的卷组的列表。 用逗号将每个用引号引起来的独立。 以下是一个示例。

    ![55-ListOfVGs][11]
 
 
17. Linux 启动时，它就会装载文件系统。 若要确保仅 Pacemaker 可以装载的 iSCSI 磁盘，重新生成的根文件系统映像。 

    运行以下命令，这可能需要一些时间才能完成。 如果成功，你将返回收到任何消息。

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. 重新启动服务器。

19. 将参与 FCI 的另一台服务器，在执行步骤 1-6。 这将为 SQL Server 中提供 iSCSI 目标。 
 
20. 生成服务器上的卷组的列表。 它应显示前面创建的卷组。 

    ```bash
    sudo vgs
    ``` 
23. 启动 SQL Server，并确认它可以在此服务器上启动。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. 停止 SQL Server 并验证它已关闭。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. 重复步骤 1 – 6 将参与 FCI 的任何其他服务器上。

现在你就可以配置 FCI。

|Distribution |主题 
|----- |-----
|**Red Hat Enterprise Linux 与 HA 外接程序** |[配置](sql-server-linux-shared-disk-cluster-configure.md)<br/>[操作](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server HA 外接程序与** |[配置](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>后续步骤

[配置故障转移群集实例-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

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
