---
title: "设备网络配置 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e2b9abe-963d-479b-a4a7-1739fcb3e249
caps.latest.revision: "27"
ms.openlocfilehash: e24ed8e992591d08628ffeb14c30a47d7fa5b54a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="appliance-network-configuration"></a>设备网络配置
SQL Server PDW 设备生成和使用修复的一组 IP 地址在所有服务器和合适的设备从 IHV 的工厂配置。 在设备的传递，必须重新配置外部 （以太网） IP 地址以匹配特定客户的数据中心的要求。  
  
> [!NOTE]  
> PDW V1 需要 8 IP 外部 (*客户面向*) 地址提供给每个控件的外部连接机架的节点。 PDW 2012 (V2) 增强了通过公开通过 IP 地址从外部设备的每个组件的网络通信。 此方法提供了更可靠的设计，这将减少成本，并增加了灵活性，并增强了数据移动、 数据加载和 Hadoop 集成。 所需的 IP 地址数取决于设备中的节点数和 hdinsight 的功能存在。 若要适应此更大的批 IP 地址，客户应单独的子网为设置 PDW。 此子网内，将有足够 IP 地址空间 （最多 250 个地址） 来容纳最多 5 PDW 机架的组件。  
  
**网络配置**页使你可以在分析平台系统设备上查看节点的面向外部的网络设置。 此页是只读的。  
  
![DWConfig 设备网络](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>若要更新你的设备上的网络配置  
通过编辑更改 fabric 域、 工作负荷域和 HDInsight 域的 IP 地址**AplianceInfo.xml**文件，然后运行安装程序。 这是脱机操作。 PDW 和 （如果存在） 的 HDInsight 区域将自动停止 IP 地址更改过程。  
  
> [!NOTE]  
> 域名在设置期间提供，指定最多 6 的字母数字字符、 以字母开头。 频繁的命名系统创建使用 F、 P，开头 PDW 工作负荷域和开头 h。 HDInsight 域启动 fabric 域此格式假定整个的帮助文件主题，但不是必需的。 <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>若要更改分析平台系统的 IP 地址  
  
1.  使用**远程桌面**应用程序中，连接到**HST01**使用工作负荷域管理员帐户。  
  
2.  在 HST01 节点上，打开设备信息文件在**c:\pdwinst\media\AplianceInfo.xml**。  
  
    > [!NOTE]  
    > 如果文件不存在，可能需要创建一个新文件。  
  
3.  以太网的 IP 值根据需要更新，并保存文件。  
  
4.  在命令提示符窗口中，执行以下的安装程序命令，以更新在 PDW 地区中，使用 P/F/H 域名和管理员密码的 IP 地址。  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>制造商引用  
有关 Dell 设备的其他信息，请参阅：  
  
-   PowerConnect 交换机说明[Dell PowerConnect 6200 系列系统 CLI 引用指南](http://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC[集成 Dell 远程访问控制器 7 (iDRAC7) 版本 1.30.30 用户指南](http://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU 的**Dell 流量机架 PDU**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>另请参阅  
[启动 Configuration Manager &#40;分析平台系统 &#41;](launch-the-configuration-manager.md)  
  
