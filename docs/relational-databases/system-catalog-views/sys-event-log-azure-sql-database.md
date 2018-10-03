---
title: sys.event_log （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- event_log
- sys.event_log_TSQL
- event_log_TSQL
- sys.event_log
dev_langs:
- TSQL
helpviewer_keywords:
- event_log
- sys.event_log
ms.assetid: ad5496b5-e5c7-4a18-b5a0-3f985d7c4758
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 29ef6eaf427a0ab8ee2a3b040f2a4255079eecdb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826345"
---
# <a name="syseventlog-azure-sql-database"></a>sys.event_log (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回成功[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]数据库连接、 连接失败和死锁。 您可以使用此信息跟踪与 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 相关的数据库活动或排除其故障。  
  
> [!CAUTION]  
>  对于具有大量的数据库或大量的登录名的安装，sys.event_log 中的活动可能会限制导致的性能，CPU 使用率过高，并可能会导致登录失败。 Sys.event_log 查询可产生的问题。 Microsoft 正在努力解决此问题。 在此期间，若要减少此问题的影响，限制 sys.event_log 查询。 NewRelic SQL Server 插件的用户应访问[Microsoft Azure SQL 数据库插件优化和性能调整](https://discuss.newrelic.com/t/microsoft-azure-sql-database-plugin-tuning-performance-tweaks/30729)有关其他配置信息。  
  
 `sys.event_log`视图包含以下各列。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|数据库的名称。 如果连接失败，并且用户未指定数据库名称，则此列为空白。|  
|**start_time**|**datetime2**|聚合间隔开始的 UTC 日期和时间。 对于聚合事件，时间始终为 5 分钟的倍数。 例如：<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|聚合间隔结束的 UTC 日期和时间。 对于聚合事件**End_time**始终是相应之后恰好 5 分钟**start_time**同一行中。 对于未聚合的事件**start_time**并**end_time**等于实际的 UTC 日期和时间的事件。|  
|**event_category**|**nvarchar(64)**|生成此事件的高级组件。<br /><br /> 请参阅[事件类型](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)有关可能的值的列表。|  
|**event_type**|**nvarchar(64)**|事件的类型。<br /><br /> 请参阅[事件类型](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)有关可能的值的列表。|  
|**event_subtype**|**int**|发生的事件的子类型。<br /><br /> 请参阅[事件类型](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)有关可能的值的列表。|  
|**event_subtype_desc**|**nvarchar(64)**|事件子类型的说明。<br /><br /> 请参阅[事件类型](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)有关可能的值的列表。|  
|severity|**int**|错误的严重性。 可能的值有：<br /><br /> 0 = 信息<br />1 = 警告<br />2 = 错误|  
|**event_count**|**int**|次数发生此事件的指定数据库中指定的时间间隔 (**start_time**并**end_time**)。|  
|**description**|**nvarchar(max)**|对事件的详细说明。<br /><br /> 请参阅[事件类型](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)有关可能的值的列表。|  
|**additional_data**|**XML**|*注意： 此值始终为 NULL 的 Azure SQL 数据库 V12。请参阅[示例](#Deadlock)部分，了解如何检索有关 V12 的死锁事件。*<br /><br /> 有关**死锁**事件，此列包含死锁图形。 对于其他事件类型，该列为 NULL。 |  
  
##  <a name="EventTypes"></a> 事件类型  
 此视图中的每一行记录的事件由类别 (**event_category**)，事件类型 (**event_type**)，和子类型 (**event_subtype**)。 下表列出了此视图中收集的事件类型。  
  
 中的事件**连接**类别，sys.database_connection_stats 视图中提供了摘要信息。  
  
> [!NOTE]  
>  此视图不包括所有可能发生的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 数据库事件，而仅限此处列出的事件。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的未来版本中可能会添加其他类别、事件类型和子类型。  
  
|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|severity|**description**|  
|-------------------------|---------------------|------------------------|------------------------------|------------------|---------------------|  
|**连接**|**connection_successful**|0|**connection_successful**|0|已成功连接到数据库。|  
|**连接**|**connection_failed**|0|**invalid_login_name**|2|登录名在此版本的 SQL Server 中无效。|  
|**连接**|**connection_failed**|1|**windows_auth_not_supported**|2|在此版本的 SQL Server 中不支持 Windows 登录名。|  
|**连接**|**connection_failed**|2|**attach_db_not_supported**|2|用户已请求附加不受支持的数据库文件。|  
|**连接**|**connection_failed**|3|**change_password_not_supported**|2|用户已请求更改不受支持的用户登录密码。|  
|**连接**|**connection_failed**|4|**login_failed_for_user**|2|用户登录失败。|  
|**连接**|**connection_failed**|5|**login_disabled**|2|登录名已禁用。|  
|**连接**|**connection_failed**|6|**failed_to_open_db**|2|*注意： 仅适用于 Azure SQL 数据库 V11。*<br /><br /> 无法打开数据库。 原因可能是该数据库不存在，或缺少身份验证而无法打开数据库。|  
|**连接**|**connection_failed**|7|**blocked_by_firewall**|2|不允许客户端 IP 地址访问该服务器。|  
|**连接**|**connection_failed**|8|**client_close**|2|*注意： 仅适用于 Azure SQL 数据库 V11。*<br /><br /> 在建立连接时，客户端可能已超时。 尝试增加连接超时值。|  
|**连接**|**connection_failed**|9|**重新配置**|2|*注意： 仅适用于 Azure SQL 数据库 V11。*<br /><br /> 连接失败，因为数据库目前正在经历重新配置。|  
|**连接**|**connection_terminated**|0|**idle_connection_timeout**|2|*注意： 仅适用于 Azure SQL 数据库 V11。*<br /><br /> 连接闲置的时间超过了系统定义的阈值。|  
|**连接**|**connection_terminated**|1|**重新配置**|2|*注意： 仅适用于 Azure SQL 数据库 V11。*<br /><br /> 由于数据库重新配置，该会话已终止。|  
|**连接**|**限制**|*\<原因代码 >*|**reason_code**|2|*注意： 仅适用于 Azure SQL 数据库 V11。*<br /><br /> 请求受到限制。  限制原因代码： *\<原因代码 >*。 有关详细信息，请参阅[引擎限制](http://msdn.microsoft.com/library/windowsazure/dn338079.aspx)。|  
|**连接**|**throttling_long_transaction**|40549|**long_transaction**|2|*注意： 仅适用于 Azure SQL 数据库 V11。*<br /><br /> 由于您有长时间运行的事务，已终止会话。 请尝试缩短您的事务的运行时间。 有关详细信息，请参阅[资源限制](http://msdn.microsoft.com/library/windowsazure/dn338081.aspx)。|  
|**连接**|**throttling_long_transaction**|40550|**excessive_lock_usage**|2|*注意： 仅适用于 Azure SQL 数据库 V11。*<br /><br /> 由于会话获取的锁过多，已终止该会话。 请尝试在单个事务中读取或修改更少的行。 有关详细信息，请参阅[资源限制](http://msdn.microsoft.com/library/windowsazure/dn338081.aspx)。|  
|**连接**|**throttling_long_transaction**|40551|**excessive_tempdb_usage**|2|*注意： 仅适用于 Azure SQL 数据库 V11。*<br /><br /> 由于过度使用 TEMPDB，已终止该会话。 请尝试修改您的查询以减少使用临时表空间。 有关详细信息，请参阅[资源限制](http://msdn.microsoft.com/library/windowsazure/dn338081.aspx)。|  
|**连接**|**throttling_long_transaction**|40552|**excessive_log_space_usage**|2|*注意： 仅适用于 Azure SQL 数据库 V11。*<br /><br /> 由于过度使用事务日志空间，已终止该会话。 请尝试在单个事务中修改更少的行。 有关详细信息，请参阅[资源限制](http://msdn.microsoft.com/library/windowsazure/dn338081.aspx)。|  
|**连接**|**throttling_long_transaction**|40553|**excessive_memory_usage**|2|*注意： 仅适用于 Azure SQL 数据库 V11。*<br /><br /> 由于过度使用内存，已终止该会话。 请尝试修改您的查询以处理更少的行。 有关详细信息，请参阅[资源限制](http://msdn.microsoft.com/library/windowsazure/dn338081.aspx)。|  
|**引擎**|**死锁**|0|**死锁**|2|发生死锁。|  
  
## <a name="permissions"></a>Permissions  
 具有访问权限的用户**主**数据库具有对此视图的只读访问。  
  
## <a name="remarks"></a>备注  
  
### <a name="event-aggregation"></a>事件聚合  
 在 5 分钟的间隔内收集和聚合此视图的事件信息。 **Event_count**列代表一个特殊的次数**event_type**并**event_subtype**某个给定的时间间隔内发生的特定数据库。  
  
> [!NOTE]  
>  某些事件（如死锁）不会聚集。 对于这些事件， **event_count**将是 1 和**start_time**并**end_time**将等于实际 UTC 日期和事件发生时的时间。  
  
 例如，如果用户在 2/5/2012 (UTC) 的 11:00 到 11:05 之间由于登录名无效而七次均无法连接到数据库 Database1，则此信息将出现在此视图的单一行内：  
  
|**database_name**|**start_time**|**end_time**|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|severity|**event_count**|**description**|**additional_data**|  
|------------------------|---------------------|-------------------|-------------------------|---------------------|------------------------|------------------------------|------------------|----------------------|---------------------|--------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`connectivity`|`connection_failed`|`4`|`login_failed_for_user`|`2`|`7`|`Login failed for user.`|`NULL`|  
  
### <a name="interval-starttime-and-endtime"></a>间隔 start_time 和 end_time  
 事件在事件发生时包含在某个聚合间隔*上*或*后 * * * start_time** 和*之前 * * * end_time** 该间隔。 例如，恰好在 `2012-10-30 19:25:00.0000000` 发生的事件将只包含在如下所示的第二个间隔内：  
  
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
  
-   此视图不包含所有[!INCLUDE[ssSDS](../../includes/sssds-md.md)]数据库会发生的错误，仅在指定的那些[事件类型](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes)本主题中。  
  
-   如果 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 数据中心内发生计算机故障，则事件表中可能缺少逻辑服务器的少量数据。  
  
-   如果通过 DoSGuard 拦截了 IP 地址，则无法收集来自该 IP 地址的连接尝试事件，这些事件不会出现在此视图中。  
  
## <a name="examples"></a>示例  
  
### <a name="simple-examples"></a>简单示例  
 以下查询将返回在 9/25/2011 与 9/28/2011 (UTC) 之间发生的所有事件。 默认情况下，查询结果按排序**start_time**顺序 （升序）。  
  
```  
SELECT * FROM sys.event_log   
WHERE start_time >= '2011-09-25 12:00:00'   
    AND end_time <= '2011-09-28 12:00:00';  
```  
  
 以下查询返回的数据库 Database1 （仅适用于 Azure SQL 数据库 V11） 的所有死锁事件。  
  
```  
SELECT * FROM sys.event_log   
WHERE event_type = 'deadlock'   
    AND database_name = 'Database1';  
```  
<a name="Deadlock"></a> 以下查询返回的数据库 Database1 （仅适用于 Azure SQL 数据库 V12） 的所有死锁事件。  
  
```  
WITH CTE AS (  
       SELECT CAST(event_data AS XML)  AS [target_data_XML]   
   FROM sys.fn_xe_telemetry_blob_target_read_file('dl', null, null, null)  
)  
SELECT target_data_XML.value('(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
target_data_XML.query('/event/data[@name=''xml_report'']/value/deadlock') AS deadlock_xml,  
target_data_XML.query('/event/data[@name=''database_name'']/value').value('(/value)[1]', 'nvarchar(100)') AS db_name  
FROM CTE   
  
```  
  
  
 以下事件对在 9/25/2011 (UTC) 的 10:00 与 11:00 之间发生的 SQL 工作线程事件返回硬中止。  
  
```  
SELECT * FROM sys.event_log   
WHERE event_type = 'throttling'   
    AND event_subtype = 4194307   
    AND start_time >= '2011-09-25 10:00:00'   
    AND end_time <= '2011-09-25 11:00:00';  
```  
  
### <a name="db-scoped-extended-event"></a>DB 范围内扩展的事件  
 下面的示例代码用于设置 db 范围内扩展的事件 (XEvent) 会话：  
  
```sql  
IF EXISTS  
    (SELECT * from sys.database_event_sessions  
        WHERE name = 'azure_monitor_deadlock_session')  
BEGIN  
    ALTER EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE  
        DROP TARGET package0.ring_buffer;  
  
    DROP EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE;  
END  
  
CREATE EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    ADD EVENT sqlserver.database_xml_deadlock_report  
    ADD TARGET package0.ring_buffer  
    (  
        SET max_memory = 2048, max_events_limit = 10  
    )  
    WITH (STARTUP_STATE = ON,  
          EVENT_RETENTION_MODE = ALLOW_SINGLE_EVENT_LOSS);  
  
ALTER EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    STATE = START;  
```  
  
### <a name="check-for-deadlock"></a>检查死锁

使用以下查询来检查是否有死锁。  
  
```sql  
WITH CTE AS (  
    SELECT CAST(xet.target_data AS XML)  AS [target_data_XML]  
        FROM            sys.dm_xe_database_session_targets AS xet  
             INNER JOIN sys.dm_xe_database_sessions        AS xe  
                 ON (xe.address = xet.event_session_address)  
        WHERE xe.name = 'azure_monitor_deadlock_session'  
)  
, CTE2 AS (  
    SELECT  
            T2.EventData.query('.').value(  
                '(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
            T2.EventData.query('.').query(  
                '(/event/data/value/deadlock)[1]')     AS deadlock_xml  
        FROM CTE  
            CROSS Apply [target_data_XML].nodes(  
                '/RingBufferTarget/event') AS T2(EventData)  
)  
SELECT * FROM CTE2;  
```  
  
## <a name="see-also"></a>请参阅  
 [Azure SQL 数据库中扩展的事件](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
  
  
