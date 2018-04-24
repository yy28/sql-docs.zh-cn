---
title: 监视并行数据仓库的加载 |Microsoft 文档
description: 通过使用分析平台系统 (AP) 管理员控制台或并行数据仓库 (PDW) 系统视图监视活动和最新的加载。"
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3230f170348f5952148894bd1fdb1ecc36a790bc
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="monitor-loads-into-parallel-data-warehouse"></a>监视器将加载到并行数据仓库
监视活动和最新[dwloader](dwloader.md)通过使用分析平台系统 (AP) 管理员控制台或并行数据仓库 (PDW) 加载[系统视图](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-reference-tsql-system-views/)。 
  
> [!TIP]  
> 通过使用 INSERT 语句或使用 SQL 语句中执行加载的商业智能工具来启动某些加载。 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>必要條件  
用于监视负载的方法，无论该登录名必须有权访问基础数据源。 

<!-- MISSING LINKS
For the permissions to grant, see “Use All of the Admin Console” in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>监视负载  
下列各节描述如何监视的加载。  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>通过使用管理控制台中监视加载  
  
1.  登录到管理员控制台。 <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  在顶部菜单中，单击**加载**。 你将看到显示所有最近的可排序表和活动负载和其他信息，如负载是否已完成或仍处于活动状态。 单击列标题来对行进行排序。  
  
3.  若要查看特定的负载的其他详细信息，请单击负载**ID**左侧列中。 在详细视图中，你可以在每个步骤中的负载中查看进度。  
  
有关在管理控制台中显示的负载有关的元数据，请参阅有关这些系统视图：  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](https://msdn.microsoft.com/library/mt203879.aspx.md)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>若要监视通过使用系统视图的加载  
若要通过使用 SQL Server PDW 的视图中监视活动和最新的加载，请按照下面的步骤。 使用每个系统视图，请参阅由视图返回的潜在值和列上的有关信息的该视图的文档。  
  
1.  查找`request_id`中负载[sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)通过查找加载程序命令行中的视图`command`此视图的列。  
  
    例如，以下命令将返回的命令文本和当前状态，加上`request_id`。  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  使用`request_id`通过检索负载的其他信息[sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) ，和[sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)视图。 例如，以下查询将返回`run_id`和信息开始日期、 结束时和持续时间的负载，以及任何错误，以及处理的行数的信息：  
  
    ```sql  
    SELECT lbr.run_id,   
    er.submit_time, er.end_time, er.total_elapsed_time, er.error_id, lbr.rows_processed, lbr.rows_rejected, lbr.rows_inserted   
    FROM sys.dm_pdw_exec_requests er   
    LEFT OUTER JOIN   
    sys.pdw_loader_backup_runs lbr   
    ON (er.request_id=lbr.requst_id)   
    WHERE er.request_id=’12738’;  
    ```  
  
<!-- MISSING LINKS

## See Also  
[Common metadata query examples](metadata-query-examples.md)
-->  
  
