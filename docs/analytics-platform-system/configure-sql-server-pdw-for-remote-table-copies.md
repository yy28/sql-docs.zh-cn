---
title: 配置远程表副本的并行数据仓库 |Microsoft 文档
description: 描述如何配置并行数据仓库以使用远程表复制功能将表复制到非设备服务器上的 SMP SQL Server 数据库。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3f71a0c67639918820bca8f6f8f38b9f354154f3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539527"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>配置远程表副本的并行数据仓库
描述如何配置 SQL Server PDW，若要使用远程表复制功能将表复制到非设备服务器上的 SMP SQL Server 数据库。  
  
本主题介绍配置远程表复制的配置步骤之一。 有关所有配置步骤的列表，请参阅[远程表复制](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>开始之前  
若要配置 SQL Server PDW 使用远程表副本，您必须：  
  
-   具有分析平台系统管理员帐户能够直接登录 ***appliance_domain *-AD01**和 ***appliance_domain *-AD02**节点。  
  
-   知道的主机名称或目标服务器的 IP 名称。  
  
## <a name="HowToPDW"></a>配置远程表副本的 SQL Server PDW： 更新在 DNS 中的主机名称  
**CREATE REMOTE TABLE**语句，用于远程表副本使用的 IP 地址或 SMP Windows 系统的 IP 名称指定目标服务器。 若要使用的 IP 名称，你需要将成功的名称解析条目添加到 DNS 服务器。  
  
以下步骤概述了如何更新 DNS 服务器。  
  
1.  登录到活动的 AD 节点 (通常 ***appliance_domain *-AD01**)。  
  
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
  
