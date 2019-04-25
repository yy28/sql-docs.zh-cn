---
title: 监视活动查询的并行数据仓库 |Microsoft Docs
description: 使用管理控制台和并行数据仓库系统视图来监视在分析平台系统上的活动查询。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d2b1ee84b2ae738d7790e1238176331a221ac473
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62640005"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>监视活动查询的并行数据仓库
本文介绍如何使用管理控制台和 SQL Server PDW 系统视图来监视活动的查询。 请参阅[通过使用管理控制台监视设备](monitor-the-appliance-by-using-the-admin-console.md)并[系统视图](tsql-system-views.md)有关这些工具的信息。  
  
## <a name="prerequisites"></a>先决条件  
而不考虑用于监视活动查询的方法，该登录名必须具有在中使用所有的"管理员控制台"中所述的权限[授予权限以使用管理控制台](grant-permissions.md#grant-permissions-to-use-the-admin-console)。  
  
## <a name="PermsAdminConsole"></a>监视活动查询  
在管理控制台和 SQL Server PDW 系统视图可用于监视活动的查询。 按照下面的说明。  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>若要通过使用管理控制台中监视活动查询  
  
1.  登录到管理员控制台。 请参阅[通过使用管理控制台监视设备](monitor-the-appliance-by-using-the-admin-console.md)有关的说明。  
  
2.  在顶部菜单中，单击**查询**。 你将看到具有最新的查询的基本信息的表上的设备，包括提交查询、 查询和查询的当前状态的开始和结束时间的登录名。  
  
3.  若要查看查询命令，请将鼠标指针悬停在该行的左侧列中的查询 ID。  
  
    若要查看有关特定查询的更多详情，请单击查询 id。 您将看到的信息包括完整的查询和查询计划，查询执行中的每个步骤的状态信息。 如果返回了任何错误，还可以在错误上查看详细的信息。 <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>若要使用系统视图来监视活动查询  
用于监视查询的主系统视图[sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。 使用此系统视图来查找`request_id`活动或最新的查询，基于查询文本。  
  
例如，以下查询查找`request_id`和当前`status`对于选择中的所有列的任何查询`memberAddresses`表。  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
之后`request_id`已被标识为一个查询，使用中的其他信息`dm_pdw_exec_requests`表，以找出有关处理的查询，或使用[sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)若要查看单个查询的状态有关查询执行的步骤。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
