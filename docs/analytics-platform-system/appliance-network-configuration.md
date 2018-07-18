---
title: 设备网络网络的分析平台系统 |Microsoft Docs
description: 生成和配置修补程序在所有服务器和从 IHV 的工厂车间适用设备的 IP 地址一 Analytics Platform System (APS) 设备。 设备的传递，时必须重新配置外部 （以太网） IP 地址以匹配特定客户的数据中心的要求。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d11184c1fd12ae40188ef4e4442e7f9b7fb6b04a
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909807"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>分析平台系统的设备的网络配置
生成和配置修补程序在所有服务器和从 IHV 的工厂车间适用设备的 IP 地址一 Analytics Platform System (APS) 设备。 设备的传递，时必须重新配置外部 （以太网） IP 地址以匹配特定客户的数据中心的要求。  
  
> [!NOTE]  
> PDW V1 所需 8 IP 外部 (*面向客户*) 地址并提供到每个控件的外部连接机架节点。 PDW 2012 (V2) 增强网络通信通过公开通过 IP 地址从外部设备的每个组件。 此方法提供了更可靠的设计，这将减少成本，并增加了灵活性，并增强了数据移动、 数据加载和 Hadoop 集成。 所需的 IP 地址数取决于设备中的节点数。 为了适应此较大的 IP 地址块，客户应设置单独的子网的 PDW。 此子网中将有足够 IP 地址空间 （最多 250 个地址） 以容纳最多 5 个 PDW 机架的组件。  
  
**网络配置**页使你可以在分析平台系统设备上查看的节点的面向外部的网络设置。 此页是只读的。  
  
![DWConfig 工具网络](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>若要更新你的设备上的网络配置  
通过编辑更改的 fabric 域和工作负荷域的 IP 地址**AplianceInfo.xml**文件，然后运行安装程序。 这是一项脱机操作。 PDW 区域 IP 地址更改期间，将自动停止。  
  
> [!NOTE]  
> 域名提供在安装过程中，指定最多 6 个字母数字字符，以字母开头。 频繁的命名系统创建从 F，PDW 工作负荷域开始第一个 fabric 域此格式假定帮助文件主题，但不是必需的。 <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>若要更改分析平台系统的 IP 地址  
  
1.  使用**远程桌面**应用程序中，连接到**HST01**使用工作负荷域管理员帐户。  
  
2.  HST01 在节点上，打开了的设备信息文件**c:\pdwinst\media\AplianceInfo.xml**。  
  
    > [!NOTE]  
    > 如果该文件不存在，可能需要创建一个新的文件。  
  
3.  根据需要更新的以太网 IP 值并保存该文件。  
  
4.  在命令提示符窗口中，执行以下的安装程序命令，以更新使用 P/F/H 域名和管理员密码的 PDW 区域的 IP 地址。  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>制造商的引用  
有关 Dell 设备的其他信息，请参阅：  
  
-   PowerConnect 开关说明[Dell PowerConnect 6200 系列系统 CLI 参考指南](http://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC[集成 Dell 远程访问控制器 7 (iDRAC7) 版本 1.30.30 用户指南](http://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU 的**Dell 按流量计费的机架 PDU**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>请参阅  
[启动配置管理器&#40;分析平台系统&#41;](launch-the-configuration-manager.md)  
  
