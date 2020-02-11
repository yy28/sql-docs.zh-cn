---
title: PDW 证书预配
description: 分析平台系统的 PDW 证书预配页 Configuration Manager 导入或删除 PDW 区域使用的证书。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 676335fb8ee4aac5906c61084c28cd94cf8ea815
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400893"
---
# <a name="pdw-certificate-provisioning---analytics-platform-system"></a>PDW 证书预配-分析平台系统
分析平台系统的**PDW 证书预配**页**Configuration Manager**导入或删除 PDW 区域使用的证书。 使用，用于加密连接的证书可通过 SQL Server 客户端、使用 SQL Server PDW 驱动程序的工具、[管理控制台](monitor-the-appliance-by-using-the-admin-console.md)和 Integration Services 负载来帮助保护与控制节点的通信。  
  
## <a name="prerequisites"></a>必备条件  
在安装证书之前，请执行以下操作：  
  
1.  获取安全证书。 如果需要有关如何获取安全证书的详细信息，请联系 Microsoft 支持部门。  
  
2.  将证书保存到受密码保护的 PFX 文件中的控制节点。  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>出于安全原因，请获取可信证书  
SQL Server PDW 支持使用证书来加密到控制节点的连接;包括到**管理控制台**的连接。  
  
默认情况下，**管理控制台**包括提供隐私的自签名证书，但不包括服务器身份验证。 这可能会使通信容易受到中间人攻击。 当用户使用自签名证书连接到管理控制台时，Internet Explorer 将返回错误： "此网站的安全证书有问题"。  
  
尽管通过自签名证书建立的连接可在客户端和服务器之间加密正在进行的数据，但是该连接仍会受到攻击者的风险。  
  
> [!WARNING]  
> 设备管理员应立即获取链接到客户端识别的受信任证书颁发机构的证书，以便建立安全连接并删除 Internet Explorer 报告的错误。  
  
证书路径必须包含映射到控制节点群集 IP 地址的完全限定域名（推荐）或用户在其浏览器地址栏中键入以访问**管理控制台**的名称。  
  
使用分析平台系统**Configuration Manager**添加或删除受信任的证书。 不支持直接使用 Microsoft Windows HTTP 服务证书配置工具（**winHttpCertCfg**）来管理证书。  
  
## <a name="import-or-remove-the-certificate"></a>导入或删除证书  
以下说明显示了如何导入或删除设备证书。

> [!WARNING]
> 若要续订过期的证书，必须先删除现有证书，然后再导入新证书。
  
### <a name="to-import-the-certificate"></a>导入证书  
  
1.  启动**Configuration Manager**。 有关详细信息，请参阅[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)。  
  
2.  在**Configuration Manager**的左窗格中，展开 "**并行数据仓库拓扑**"，然后单击 "**证书**"。  
  
3.  选择 **"导入证书" 并将设备配置为使用该证书**，然后单击 "**浏览**" 浏览到并选择证书文件。  
  
4.  在 "**密码**" 字段中输入证书的密码。  
  
5.  单击 "**应用**"，为设备配置证书。  
  
SQL Server PDW 将不使用导入的证书加密当前连接，但会将证书用于新连接。  
  
### <a name="to-remove-the-previously-imported-certificate"></a>删除以前导入的证书  
  
1.  启动**Configuration Manager**。 有关详细信息，请参阅[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)。  
  
2.  在**Configuration Manager**的左窗格中，展开 "**并行数据仓库拓扑**"，然后单击 "**证书**"。  
  
3.  选择 **"删除设备中预配的任何证书"**。  
  
4.  单击 "**应用**"，从设备中删除以前导入的证书。  
  
SQL Server PDW 将继续加密当前连接，但不会将删除的证书用于新连接。  
  
![DWConfig 工具 PDW 证书](./media/pdw-certificate-provisioning/SQL_Server_PDW_DWConfig_ApplPDWCert.png "SQL_Server_PDW_DWConfig_ApplPDWCert")  
  
## <a name="see-also"></a>另请参阅  
[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)  
<!-- MISSING LINKS [HDInsight Certificate Provisioning &#40;Analytics Platform System&#41;](hdinsight-certificate-provisioning.md)  -->  
  
