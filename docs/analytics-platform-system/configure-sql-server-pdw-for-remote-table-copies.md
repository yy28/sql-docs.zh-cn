---
title: 为远程表副本配置并行数据仓库 |Microsoft Docs
description: 介绍如何配置并行数据仓库，以使用远程表复制功能将表复制到非设备服务器上的 SMP SQL Server 数据库。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: fdac0b6ed211e223c3fad7ba15ac79a282c61303
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509519"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>并行数据仓库配置为远程表副本
介绍如何配置 SQL Server PDW 使用远程表复制功能，将表复制到非设备服务器上的 SMP SQL Server 数据库。  
  
本主题介绍配置远程表复制的配置步骤之一。 所有配置步骤的列表，请参阅[远程表复制](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>开始之前  
若要配置 SQL Server PDW 使用远程表副本，您必须：  
  
-   分析平台系统管理员帐户能够登录直接到具有 <strong>*appliance_domain*-AD01</strong>并 <strong>*appliance_domain*-AD02</strong>节点。  
  
-   知道的主机名或 IP 的目标服务器的名称。  
  
## <a name="HowToPDW"></a>配置 SQL Server PDW 的远程表副本：在 DNS 中更新主机名  
**CREATE REMOTE TABLE**语句，用于远程表副本使用的 IP 地址或 SMP Windows 系统的 IP 名称指定目标服务器。 若要使用的 IP 名称，您需要将成功的名称解析的条目添加到 DNS 服务器。  
  
以下步骤概述了如何更新 DNS 服务器。  
  
1.  登录到 active AD 节点 (通常 <strong>*appliance_domain*-AD01</strong>)。  
  
2.  打开 DNS 管理器。 该文件位于下**管理工具**中**启动**菜单。  
  
3.  使用 DNS 管理器添加的 IP 名称。  
  
## <a name="see-also"></a>请参阅  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[使用 DNS 转发器解析非设备 DNS 名称](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
