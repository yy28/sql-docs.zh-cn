---
title: sys.database_connection_stats （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 03/25/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_connection_stats
- database_connection_stats
- database_connection_stats_TSQL
- sys.database_connection_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_connection_stats
- database_connection_stats
ms.assetid: 5c8cece0-63b0-4dee-8db7-6b43d94027ec
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 801074dd7e82f5e1564564125486e0845e2303fb
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2018
ms.locfileid: "53589478"
---
# <a name="sysdatabaseconnectionstats-azure-sql-database"></a>sys.database_connection_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  包含的统计信息[!INCLUDE[ssSDS](../../includes/sssds-md.md)]数据库**连接**事件，提供数据库连接成功和失败的概述。 有关连接事件的详细信息，请参阅中的事件类型[sys.event_log &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md)。  
  
|统计信息|类型|Description|  
|---------------|----------|-----------------|  
|**database_name**|**sysname**|数据库的名称。|  
|**start_time**|**datetime2**|聚合间隔开始的 UTC 日期和时间。 时间始终为 5 分钟的倍数。 例如：<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|聚合间隔结束的 UTC 日期和时间。 **End_time**始终是相应之后恰好 5 分钟**start_time**同一行中。|  
|**success_count**|**int**|成功连接数。|  
|**total_failure_count**|**int**|失败连接的总数。 这是总和**connection_failure_count**， **terminated_connection_count**，并**throttled_connection_count**，并且不包括死锁事件。|  
|**connection_failure_count**|**int**|登录失败数。|  
|**terminated_connection_count**|**int**|**_仅适用于[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]v11。_**<br /><br /> 终止连接数。|  
|**throttled_connection_count**|**int**|**_仅适用于[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]v11。_**<br /><br /> 中止的连接数。|  
  
## <a name="remarks"></a>备注  
  
### <a name="event-aggregation"></a>事件聚合  
 在 5 分钟的间隔内收集和聚合此视图的事件信息。 计数列表示特定连接事件在给定的时间间隔内针对特定数据库发生的次数。  
  
 例如，如果用户在 2/5/2012 (UTC) 的 11:00 到 11:05 之间七次均无法连接到数据库 Database1，则此信息将出现在此视图的单一行内：  
  
|**database_name**|**start_time**|**end_time**|**success_count**|**total_failure_count**|**connection_failure_count**|**terminated_connection_count**|**throttled_connection_count**|  
|------------------------|---------------------|-------------------|------------------------|-------------------------------|------------------------------------|---------------------------------------|--------------------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`0`|`7`|`7`|`0`|`0`|  
  
### <a name="interval-starttime-and-endtime"></a>间隔 start_time 和 end_time  
 事件在事件发生时包含在某个聚合间隔*上*或_后_**start_time**并_之前_**end_time**该间隔。 例如，恰好在 `2012-10-30 19:25:00.0000000` 发生的事件将只包含在如下所示的第二个间隔内：  
  
```  
  
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```  
  
### <a name="data-updates"></a>数据更新  
 此视图中的数据会随时间推移而累积。 通常，数据将在聚合间隔开始后的一小时内累积，但可能需要多达 24 小时才能使所有数据都出现在此视图中。 在此期间，可能会定期更新单一行中的信息。  
  
### <a name="data-retention"></a>数据保持期  
 视图中的数据将保留最多 30 天或可能更少时间，具体取决于逻辑服务器中的数据库数量和每个数据库生成的唯一事件数量。 要将此信息保留更长期间，请将数据复制到单独的数据库。 在对视图进行初始复制后，视图中的行可能会随数据的累积而进行更新。 为了使数据副本保持最新状态，请定期对表中的行进行扫描，以查看现有行的事件计数的增加并确定新行（您可以通过使用开始时间和结束时间来确定唯一的行），然后使用这些更改更新您的数据副本。  
  
### <a name="errors-not-included"></a>未包括的错误  
 此视图可能并未包含所有连接和错误信息：  
  
-   此视图不包含所有[!INCLUDE[ssSDS](../../includes/sssds-md.md)]数据库可能会发生，仅那些中的事件类型中指定的错误[sys.event_log &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md)。  
  
-   如果 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 数据中心内发生计算机故障，则事件表中可能缺少逻辑服务器的少量数据。  
  
-   如果通过 DoSGuard 拦截了 IP 地址，则无法收集来自该 IP 地址的连接尝试事件，这些事件不会出现在此视图中。  
  
## <a name="permissions"></a>权限  
 具有访问权限的用户**主**数据库具有对此视图的只读访问。  
  
## <a name="example"></a>示例  
 下面的示例演示的查询**sys.database_connection_stats**返回中午 2011 年 9 月 25 日中午 9/28/2011 (UTC) 之间发生的数据库连接的摘要。 默认情况下，查询结果按排序**start_time**顺序 （升序）。  
  
```  
SELECT *  
FROM sys.database_connection_stats   
WHERE start_time>='2011-09-25:12:00:00' and end_time<='2011-09-28 12:00:00';  
```  
  
## <a name="see-also"></a>请参阅  
 [Windows Azure SQL 数据库故障排除](https://msdn.microsoft.com/library/windowsazure/ee730906.aspx)  
  
  
