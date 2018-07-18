---
title: 远程表复制的并行数据仓库 |Microsoft 文档
description: 使用分析平台系统并行数据仓库中的远程表复制。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5ed517a471368e4192ad7393a92274424d37f975
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538717"
---
# <a name="remote-table-copy"></a>远程表复制
描述如何使用远程表复制功能将从 SQL Server PDW 数据库的表复制到远程的 （非设备） SMP SQL Server 数据库。 用于 SQL Server PDW 的远程表复制到启用中心辐射方案。  
  
## <a name="BasicsPDE"></a>理解 SQL Server PDW 远程表复制  
远程表复制是通过将 SQL SELECT 语句的结果复制到 SMP 数据库的表中支持中心辐射方案的 SQL Server PDW 的功能。 使用启动远程表复制[远程 TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md)语句。  
  
## <a name="BasicsPrerequisites"></a>使用远程表复制的要求  
满足这些条件时，你可以使用从 SQL Server PDW 到 SQL Server 数据库的远程表复制到复制表：  
  
-   目标数据库必须是 Microsoft® SQL Server® Microsoft Windows® 系统可以连接到 SQL Server PDW 设备，但不是位于在设备中的服务器运行的实例。 远程 SQL Server 可以连接到 SQL Server PDW 使用 InfiniBand 网络或通过以太网网络。  
  
-   要复制的数据必须是可选择使用单个的有效 SQL Server PDW[选择](../t-sql/queries/select-transact-sql.md)语句。  
  
-   目标服务器必须为非设备服务器。 数据无法直接从一个设备复制到另一个使用本主题中的说明。  
  
-   目标服务器必须可以访问设备的无限带宽网络上的所有节点。  
  
## <a name="ConfigureRemote"></a>配置远程表副本  
若要使用远程表复制，你需要购买和配置 Windows 服务器、 配置 SQL Server 在 Windows server 中，并配置 SQL Server PDW。 使用以下链接来执行以下三个配置步骤。  
  
1.  [外部 Windows 将系统配置为接收远程表副本使用 InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [配置外部 SMP SQL 服务器以接收远程表副本](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [配置远程表副本的 SQL Server PDW](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>执行远程表复制  
若要执行远程表复制，使用[远程 TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL 语句。 示例包括附带 CREATE REMOTE TABLE 主题。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
