---
title: 监视活动查询
description: 使用管理控制台和并行数据仓库系统视图监视分析平台系统上的活动查询。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9157db745b999711966f0019747ba1d61823569e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400916"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>监视活动查询-并行数据仓库
本文介绍如何使用管理控制台和 SQL Server PDW 系统视图来监视活动的查询。 请参阅 [使用管理控制台](monitor-the-appliance-by-using-the-admin-console.md) 和 [系统视图](tsql-system-views.md) 监视设备，了解有关这些工具的信息。  
  
## <a name="prerequisites"></a>先决条件  
不管使用哪种方法来监视活动查询，登录名必须具有 "使用所有管理控制台" 中所述的权限 [才能使用管理控制台](grant-permissions.md#grant-permissions-to-use-the-admin-console)。  
  
## <a name="monitor-active-queries"></a><a name="PermsAdminConsole"></a>监视活动查询  
可以使用管理控制台和 SQL Server PDW 系统视图来监视活动的查询。 请根据以下说明操作。  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>使用管理控制台监视活动查询  
  
1.  登录到管理控制台。 有关说明，请参阅 [使用管理控制台监视设备](monitor-the-appliance-by-using-the-admin-console.md) 。  
  
2.  在顶部菜单中，单击 " **查询**"。 你将看到一个表，其中包含有关设备上最新查询的基本信息，包括提交查询的登录名、查询的开始和结束时间，以及查询的当前状态。  
  
3.  若要查看 query 命令，请将鼠标指针悬停在该行左侧列中的查询 ID 上。  
  
    若要查看特定查询的详细信息，请单击 "查询 ID"。 您将看到包含完整查询和查询计划的信息，其中包含查询执行中每个步骤的状态信息。 如果返回了任何错误，还可以查看有关错误的详细信息。 <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>使用系统视图监视活动查询  
用于监视查询的主系统视图为 [sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。 使用此系统视图可以 `request_id` 基于查询文本查找活动或最近查询的。  
  
例如，下面的查询将查找 `request_id` `status` 从表中选择所有列的任何查询的和当前 `memberAddresses` 。  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
`request_id`为查询标识后，请使用表中的其他信息 `dm_pdw_exec_requests` 来了解有关查询的处理情况，或使用[sys. dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)查看查询执行的各个查询步骤的状态。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
