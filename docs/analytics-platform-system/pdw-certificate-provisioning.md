---
title: PDW 证书预配的分析平台系统 |Microsoft Docs
description: PDW 证书预配的分析平台系统配置管理器的页导入或删除的 PDW 区域使用的证书。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 48ad2aed20f497c8400727d9d217dc8f467ac492
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960439"
---
# <a name="pdw-certificate-provisioning---analytics-platform-system"></a>PDW 证书预配的分析平台系统
**PDW 证书预配**页的分析平台系统**Configuration Manager**导入或删除的 PDW 区域使用的证书。 使用，对通信进行加密的证书可以帮助保护通信到控制节点通过 SQL Server 客户端，使用 SQL Server PDW 驱动程序的工具[管理员控制台](monitor-the-appliance-by-using-the-admin-console.md)，和 Integration Services 将加载。  
  
## <a name="prerequisites"></a>系统必备  
之前安装证书，请执行以下操作：  
  
1.  获取安全证书。 如果需要有关如何获取安全证书的详细信息，请联系 Microsoft 支持部门。  
  
2.  将证书保存到受密码保护的 PFX 文件中的控制节点。  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>对于安全原因，获取受信任的证书  
SQL Server PDW 支持使用证书来加密连接到控制节点;包括连接到**管理员控制台**。  
  
默认情况下**管理员控制台**包含一个自签名的证书，它提供的隐私，但不是服务器身份验证。 这可以使通信容易遭受拦截的攻击。 当用户连接到管理控制台通过使用自签名的证书时，Internet Explorer 将返回错误："没有此网站的安全证书有问题"。  
  
尽管自签名证书通过连接对客户端和服务器之间传输的数据的数据进行加密，则连接是仍面临攻击的风险。  
  
> [!WARNING]  
> 设备管理员应立即获取证书链接至受信任的证书颁发机构的客户端，以便建立安全连接，并删除 Internet Explorer 报告的错误识别。  
  
证书路径必须包含完全限定的域名映射到控制节点群集 IP 地址 （推荐） 或用户向它们访问的浏览器地址栏中键入的名称**管理员控制台**。  
  
使用 Analytics Platform System**Configuration Manager**添加或删除受信任的证书。 直接使用 Microsoft Windows HTTP 服务证书配置工具 (**winHttpCertCfg.exe**) 若要管理的证书不受支持。  
  
## <a name="import-or-remove-the-certificate"></a>导入或删除证书  
以下说明介绍如何导入或删除设备证书。

> [!WARNING]
> 若要续订过期的证书必须导入新之前删除现有证书。
  
### <a name="to-import-the-certificate"></a>若要将证书导入  
  
1.  启动**配置管理器**。 有关详细信息，请参阅[启动配置管理器&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在左窗格中**Configuration Manager**，展开**并行数据仓库拓扑**，然后单击**证书**。  
  
3.  选择**导入证书和配置的设备，可使用它**，然后单击**浏览**以浏览到并选择证书文件。  
  
4.  输入证书的密码**密码**字段。  
  
5.  单击**应用**配置设备的证书。  
  
SQL Server PDW 不将对当前连接使用导入的证书进行加密，但将对新的连接使用的证书。  
  
### <a name="to-remove-the-previously-imported-certificate"></a>若要删除以前导入的证书  
  
1.  启动**配置管理器**。 有关详细信息，请参阅[启动配置管理器&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在左窗格中**Configuration Manager**，展开**并行数据仓库拓扑**，然后单击**证书**。  
  
3.  选择**删除设备中预配任何证书**。  
  
4.  单击**应用**从设备中删除以前导入的证书。  
  
SQL Server PDW 将继续当前的连接进行加密，但不是会使用已删除的证书进行新连接。  
  
![DWConfig 工具 PDW 证书](./media/pdw-certificate-provisioning/SQL_Server_PDW_DWConfig_ApplPDWCert.png "SQL_Server_PDW_DWConfig_ApplPDWCert")  
  
## <a name="see-also"></a>请参阅  
[启动配置管理器&#40;分析平台系统&#41;](launch-the-configuration-manager.md)  
<!-- MISSING LINKS [HDInsight Certificate Provisioning &#40;Analytics Platform System&#41;](hdinsight-certificate-provisioning.md)  -->  
  
