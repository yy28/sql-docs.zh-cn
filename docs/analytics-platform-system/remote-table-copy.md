---
title: 远程表副本
description: 使用分析平台系统并行数据仓库中的远程表复制。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ecbbdced731e940de46dbde4a65adc486f602c2f
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400482"
---
# <a name="remote-table-copy"></a>远程表复制
描述如何使用远程表复制功能将表从 SQL Server PDW 数据库复制到远程 (非设备) SMP SQL Server 数据库。 使用远程表复制可以启用 SQL Server PDW 的中心和辐射方案。  
  
## <a name="understand-remote-table-copy-for-sql-server-pdw"></a><a name="BasicsPDE"></a>了解 SQL Server PDW 的远程表副本  
远程表复制是 SQL Server PDW 的一项功能，它通过将 SQL SELECT 语句的结果复制到 SMP 数据库中的表来实现中心辐射和辐射方案。 远程表复制是通过 [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) 语句启动的。  
  
## <a name="requirements-for-using-remote-table-copy"></a><a name="BasicsPrerequisites"></a>使用远程表复制的要求  
满足这些条件时，可以使用 "远程表复制" 将表从 SQL Server PDW 复制到 SQL Server 数据库：  
  
-   目标数据库必须是 Microsoft® SQL Server®的实例，该实例在可以连接到 SQL Server PDW 设备但不驻留在设备中的 Microsoft Windows®系统上运行。 远程 SQL Server 可以使用 "未受使用的网络" 或通过以太网连接到 SQL Server PDW。  
  
-   必须使用单个有效 SQL Server PDW [SELECT](../t-sql/queries/select-transact-sql.md) 语句来选择要复制的数据。  
  
-   目标服务器必须为非设备服务器。 使用本主题中的说明无法将数据直接从一个设备复制到另一台设备。  
  
-   对于设备的未受网络的所有节点，必须可访问目标服务器。  
  
## <a name="configure-remote-table-copy"></a><a name="ConfigureRemote"></a>配置远程表复制  
若要使用远程表复制，需要购买并配置 Windows server，在 Windows server 上配置 SQL Server，并配置 SQL Server PDW。 使用以下链接来执行这三个配置步骤。  
  
1.  [将外部 Windows 系统配置为使用无带宽接收远程表副本](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [配置外部 SMP SQL Server 以接收远程表副本](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [为远程表副本配置 SQL Server PDW](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="perform-a-remote-table-copy"></a><a name="PerformRemote"></a>执行远程表复制  
若要执行远程表复制，请使用 [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL 语句。 创建远程表主题中包含了示例。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
