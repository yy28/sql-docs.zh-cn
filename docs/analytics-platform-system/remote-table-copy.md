---
title: 远程表复制-并行数据仓库 |Microsoft Docs
description: 分析平台系统并行数据仓库中使用远程表副本。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 28bd5deda25650d36467281ccbffa7b666f4c695
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960206"
---
# <a name="remote-table-copy"></a>远程表复制
介绍如何使用远程表复制功能将表从 SQL Server PDW 的数据库复制到远程的 （非设备） SMP SQL Server 数据库。 使用 SQL Server PDW 远程表复制到启用中心和分支方案。  
  
## <a name="BasicsPDE"></a>了解适用于 SQL Server PDW 的远程表复制  
远程表复制是一项功能的 SQL Server PDW，以通过将 SQL SELECT 语句的结果复制到 SMP 数据库的表中实现中心辐射方案。 使用启动的远程表副本[REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md)语句。  
  
## <a name="BasicsPrerequisites"></a>使用远程表复制的要求  
满足这些条件时，可以使用从 SQL Server PDW 到 SQL Server 数据库的远程表复制到复制表：  
  
-   目标数据库必须是可以连接到 SQL Server PDW 设备，但未驻留在设备中的服务器上的 Microsoft Windows® 系统运行的 Microsoft® SQL Server® 的实例。 远程 SQL Server 可以连接到 SQL Server PDW 使用 InfiniBand 网络或通过以太网网络。  
  
-   要复制的数据必须是可选择使用单一的有效 SQL Server PDW[选择](../t-sql/queries/select-transact-sql.md)语句。  
  
-   目标服务器必须为非设备服务器。 数据不能直接从一个设备复制到另一个使用本主题中的说明。  
  
-   目标服务器必须可以访问设备的 Infiniband 网络上的所有节点。  
  
## <a name="ConfigureRemote"></a>将远程表副本配置  
若要使用远程表复制，您需要购买并配置 Windows 服务器，在 Windows 服务器上，配置 SQL Server 和配置 SQL Server PDW。 使用以下链接可执行以下三个配置步骤。  
  
1.  [配置外部 Windows 系统以接收使用 InfiniBand 的远程表副本](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [配置外部 SMP SQL Server 以接收远程表副本](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [配置 SQL Server PDW 的远程表副本](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>执行远程表复制  
若要执行的远程表副本，请使用[REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL 语句。 CREATE REMOTE TABLE 主题包含示例。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
