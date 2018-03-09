---
title: "PDW 证书设置 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a423b7d-c6ea-45c1-80b0-26758170594c
caps.latest.revision: "22"
ms.openlocfilehash: 9abee9638492368fe407f98a81beea2a48148971
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="pdw-certificate-provisioning"></a>PDW 证书设置
**PDW 证书预配**Analytics Platform System 页**Configuration Manager**导入或删除 PDW 区域使用的证书。 使用，对通信进行加密的证书有助于给控制节点通过 SQL Server 客户端，使用 SQL Server PDW 驱动程序的工具的安全通信[管理控制台](monitor-the-appliance-by-using-the-admin-console.md)，并 Integration Services 将加载。  
  
## <a name="prerequisites"></a>必备条件  
然后再安装证书，请执行以下操作：  
  
1.  获取安全证书。 如果你需要有关如何获取安全证书的详细信息，请联系 Microsoft 支持部门。  
  
2.  将证书保存到受密码保护的 PFX 文件中的控件节点。  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>对于安全原因，获取受信任的证书  
SQL Server PDW 支持使用证书来加密连接到管理节点中;包括连接到**管理控制台**。  
  
默认情况下，**管理控制台**包括自签名的证书，它提供的隐私，但不是服务器的身份验证。 这可以使通信容易遭受拦截的攻击。 当用户连接到管理员控制台通过使用自签名的证书时，Internet Explorer 将返回错误:"没有此网站的安全证书有问题"。  
  
尽管连接通过自签名证书对客户端和服务器之间的正在进行数据进行加密，但连接仍然是来自的攻击者的风险。  
  
> [!WARNING]  
> 设备管理员应立即获取证书链接至受信任的证书颁发机构的客户端，以便建立的安全连接并删除 Internet 资源管理器报告的错误识别。  
  
证书路径的完全限定的域名映射到控制节点群集 IP 地址 （推荐） 或用户在访问其浏览器地址栏中键入的名称必须包含**管理控制台**。  
  
使用分析平台系统**Configuration Manager**添加或删除受信任的证书。 直接使用 Microsoft Windows HTTP Services 证书配置工具 (**winHttpCertCfg.exe**) 来管理证书不受支持。  
  
## <a name="import-or-remove-the-certificate"></a>导入或删除证书  
下面的说明演示如何导入或删除设备证书。  
  
### <a name="to-import-the-certificate"></a>导入证书  
  
1.  启动**Configuration Manager**。 有关详细信息，请参阅[启动 Configuration Manager &#40;分析平台系统 &#41;](launch-the-configuration-manager.md).  
  
2.  在左窗格中**Configuration Manager**，展开**并行数据仓库拓扑**，然后单击**证书**。  
  
3.  选择**导入证书和配置设备以使用它**，然后单击**浏览**以浏览到并选择证书文件。  
  
4.  输入中的证书的密码**密码**字段。  
  
5.  单击**应用**配置设备的证书。  
  
SQL Server PDW 不会通过使用导入的证书，加密当前连接，但将使用新连接的证书。  
  
### <a name="to-remove-the-previously-imported-certificate"></a>若要删除以前导入的证书  
  
1.  启动**Configuration Manager**。 有关详细信息，请参阅[启动 Configuration Manager &#40;分析平台系统 &#41;](launch-the-configuration-manager.md).  
  
2.  在左窗格中**Configuration Manager**，展开**并行数据仓库拓扑**，然后单击**证书**。  
  
3.  选择**删除设备中的任何证书**。  
  
4.  单击**应用**从设备中删除以前导入的证书。  
  
SQL Server PDW 加密当前连接，将继续，但将不使用已删除的证书进行新的连接。  
  
![DWConfig 设备 PDW 证书](./media/pdw-certificate-provisioning/SQL_Server_PDW_DWConfig_ApplPDWCert.png "SQL_Server_PDW_DWConfig_ApplPDWCert")  
  
## <a name="see-also"></a>另请参阅  
[启动 Configuration Manager &#40;分析平台系统 &#41;](launch-the-configuration-manager.md)  
<!-- MISSING LINKS [HDInsight Certificate Provisioning &#40;Analytics Platform System&#41;](hdinsight-certificate-provisioning.md)  -->  
  
