---
title: "配置 SQL Server PDW 的远程表副本 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 496b4214-5891-404c-8237-c2a1e09db6d5
caps.latest.revision: "11"
ms.openlocfilehash: 5daa546ed4cf0eeed1c51713fd9e55aa88515380
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="configure-sql-server-pdw-for-remote-table-copies"></a>配置远程表副本的 SQL Server PDW
描述如何配置 SQL Server PDW，若要使用远程表复制功能将表复制到非设备服务器上的 SMP SQL Server 数据库。  
  
本主题介绍配置远程表复制的配置步骤之一。 有关所有配置步骤的列表，请参阅[远程表复制](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>开始之前  
若要配置 SQL Server PDW 使用远程表副本，您必须：  
  
-   具有分析平台系统管理员帐户能够直接登录 ***appliance_domain*-AD01**和 ***appliance_domain*-AD02**节点。  
  
-   知道的主机名称或目标服务器的 IP 名称。  
  
## <a name="HowToPDW"></a>配置远程表副本的 SQL Server PDW： 更新在 DNS 中的主机名称  
**CREATE REMOTE TABLE**语句，用于远程表副本使用的 IP 地址或 SMP Windows 系统的 IP 名称指定目标服务器。 若要使用的 IP 名称，你需要将成功的名称解析条目添加到 DNS 服务器。  
  
以下步骤概述了如何更新 DNS 服务器。  
  
1.  登录到活动的 AD 节点 (通常 ***appliance_domain*-AD01**)。  
  
2.  打开 DNS 管理器。 这位于**管理工具**中**启动**菜单。  
  
3.  使用 DNS 管理器中添加的 IP 名称。  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[使用 DNS 转发器来解析非设备 DNS 名称](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
