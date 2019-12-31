---
title: 设备网络配置
description: 分析平台系统（AP）设备是在所有服务器和来自 IHV 工厂的工厂中使用的一组 IP 地址的修补程序构建和配置的。 交付设备后，必须重新配置外部（以太网） IP 地址，使之与特定客户的数据中心需求相匹配。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: af892cbb43b42953732bda59d371e3e22855413b
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401413"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>用于分析平台系统的设备网络配置
分析平台系统（AP）设备是在所有服务器和来自 IHV 工厂的工厂中使用的一组 IP 地址的修补程序构建和配置的。 交付设备后，必须重新配置外部（以太网） IP 地址，使之与特定客户的数据中心需求相匹配。  
  
> [!NOTE]  
> PDW V1 需要8个 IP 外部（*面向客户*）地址，以提供与每个控制机架节点的外部连接。 PDW 2012 （V2）通过 IP 地址向外公开设备的每个组件，增强了网络通信。 此方法提供了一种更可靠的设计，可降低成本、提高灵活性，并增强数据移动、数据加载和 Hadoop 集成。 所需的 IP 地址数取决于设备中的节点数。 为了容纳这一较大的 IP 地址块，客户应为 PDW 设置一个单独的子网。 在此子网中，会有足够的 IP 地址空间（最多250个地址）来容纳最多5个 PDW 机架的组件。  
  
通过 "**网络配置**" 页，可以查看针对分析平台系统设备上的节点的面向外部的网络设置。 此页为只读。  
  
![DWConfig 工具网络](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>更新设备上的网络配置  
通过编辑**AplianceInfo**文件，然后运行安装程序，更改 fabric 域和工作负荷域的 IP 地址。 这是一种脱机操作。 在 IP 地址更改过程中，PDW 区域将自动停止。  
  
> [!NOTE]  
> 域名是在安装过程中提供的，并指定为最多6个字母数字字符（以字母开头）。 通常，命名系统将创建从 F 开始的结构域，该域从 P 开始。此格式在整个帮助文件主题中都是假设，但并不是必需的。 <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>更改分析平台系统的 IP 地址  
  
1.  使用**远程桌面**应用程序，使用工作负荷域管理员帐户连接到**HST01** 。  
  
2.  在 HST01 节点上，在**c:\pdwinst\media\AplianceInfo.xml**中打开设备信息文件。  
  
    > [!NOTE]  
    > 如果该文件不存在，则可能需要创建新的文件。  
  
3.  根据需要更新以太网 IP 值，并保存该文件。  
  
4.  在命令提示符窗口中，执行以下安装程序命令，以使用 P/F/H 域名和管理员密码更新 PDW 区域的 IP 地址。  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>制造商参考  
有关戴尔设备的其他信息，请参阅：  
  
-   PowerConnect 交换机说明[Dell PowerConnect 6200 系列系统 CLI 参考指南](https://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC[集成 Dell 远程访问控制器7（iDRAC7）版本1.30.30 用户指南](https://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU 的**Dell 计量机架 pdu**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>另请参阅  
[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)  
  
