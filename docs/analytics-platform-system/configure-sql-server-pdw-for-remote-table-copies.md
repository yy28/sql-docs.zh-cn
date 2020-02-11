---
title: 远程表副本
description: 介绍如何将并行数据仓库配置为使用远程表复制功能将表复制到非设备服务器上的 SMP SQL Server 数据库。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6c9a0a29b543eb287c7e233d6b1ea77bb2a0d45c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401267"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>为远程表副本配置并行数据仓库
描述如何将 SQL Server PDW 配置为使用远程表复制功能将表复制到非设备服务器上的 SMP SQL Server 数据库。  
  
本主题介绍配置远程表复制的配置步骤之一。 有关所有配置步骤的列表，请参阅[远程表复制](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>开始之前  
若要配置 SQL Server PDW 以使用远程表复制，必须执行以下操作：  
  
-   让一个分析平台系统管理员帐户能够直接登录到<strong> *appliance_domain*-AD01</strong>和<strong> *appliance_domain*AD02</strong>节点。  
  
-   了解目标服务器的主机名或 IP 名称。  
  
## <a name="HowToPDW"></a>配置远程表复制 SQL Server PDW：更新 DNS 中的主机名  
**CREATE REMOTE table**语句用于远程表复制，使用 SMP Windows 系统的 ip 地址或 ip 名称指定目标服务器。 若要使用 IP 名称，需要将成功的名称解析条目添加到 DNS 服务器。  
  
以下步骤概述了如何更新 DNS 服务器。  
  
1.  登录到活动 AD 节点（通常<strong> *appliance_domain*-AD01</strong>）。  
  
2.  打开 DNS 管理器。 这位于 "**开始**" 菜单中的 "**管理工具**" 下。  
  
3.  使用 DNS 管理器添加 IP 名称。  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[使用 DNS 转发器解析非设备 DNS 名称](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
