---
title: 直方图目标 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- bucketing target [SQL Server extended events]
- event bucketing target
- targets [SQL Server extended events], bucketing
ms.assetid: 2ea39141-7eb0-4c74-abf8-114c2c106a19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a584311061a24d674eed114f37d9cbbbda43909
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064703"
---
# <a name="histogram-target"></a>直方图目标
  直方图目标基于事件数据对发生的特定事件类型进行分组。 事件的分组是基于指定的事件列或操作进行计数的。 您可以使用直方图目标来排除性能问题。 通过标识哪些事件发生的频率最高，您就可以找到可能引起性能问题的“作用点”。  
  
 下表描述了可用于配置直方图目标的选项。  
  
|Option|允许的值|Description|  
|------------|--------------------|-----------------|  
|slots|任何整数值。 该值是可选的。|用户指定值，指示要保留的分组的最大数目。 达到此值后，将忽略那些不属于现有组的新事件。<br /><br /> 请注意，为了提高性能，槽号将向上舍入到最近的 2 次幂。|  
|filtering_event_name|扩展事件会话中存在的任何事件。 该值是可选的。|用于标识事件类的用户指定值。 只有指定事件实例才会存储在桶中。 所有其他事件都被忽略。<br /><br /> 如果指定此值，则必须使用以下格式： *package_name*.*event_name*，例如 `'sqlserver.checkpoint_end'`。 使用以下查询可以标识包名称：<br /><br /> 选择 p.name、 se.event_name<br />从 sys.dm_xe_session_events se<br />加入 sys.dm_xe_packages p<br />ON se_event_package_guid = p.guid<br />ORDER BY p.name、 se.event_name<br /><br /> <br /><br /> 如果不指定 filtering_event_name 值，则必须将 source_type 设为 1（默认值）。|  
|source_type|存储桶基于的对象的类型。 该值是可选的，如果未指定值，则使用默认值 1。|可以是下列值之一：<br /><br /> 0 = 事件<br /><br /> 1 = 操作|  
|源 (source)|事件列或操作名称。|用作数据源的事件列或操作名称。<br /><br /> 当为源指定事件列时，必须从用作 filtering_event_name 值的事件中指定列。 使用以下查询可以标识潜在列：<br /><br /> SELECT name FROM sys.dm_xe_object_columns<br />WHERE object_name = '\<eventname>'<br />AND column_type != 'readonly'<br /><br /> 当为源指定事件列时，不一定要在源值中包括包名称。<br /><br /> 当为源指定操作名称时，必须使用在此目标所用于的事件会话中为收集配置的一个操作。 若要查找操作名称的潜在值，可以查询 sys.dm_xe_sesssion_event_actions 视图的 action_name 列。<br /><br /> 如果将操作名称作为数据源使用，则必须使用以下格式指定源值： *package_name*.*action_name*。|  
  
 以下示例演示了直方图目标如何在高级别收集数据。 在此示例中，您希望使用直方图目标来计算每种等待类型中发生的等待数。 为此，您将会在定义直方图目标时指定以下选项：  
  
-   filtering_event_name = 'wait_info'  
  
-   source = 'wait_type'  
  
-   source_type = 0（因为 wait_type 是个事件列）  
  
 在此示例方案中，针对 wait_type 源记录了以下数据。  
  
|筛选事件名称|源列值|  
|--------------------------|-------------------------|  
|wait_info|file_io|  
|wait_info|file_io|  
|wait_info|网络|  
|wait_info|网络|  
|wait_info|sleep|  
  
 等待类型值可以划分为三个槽，具有以下值和槽计数：  
  
|ReplTest1|槽计数|  
|-----------|----------------|  
|file_io|2|  
|网络|2|  
|sleep|1|  
  
 直方图目标只保留指定源的事件数据。 某些情况下，事件数据可能太大而无法完全保留，这时便会截断数据。 截断事件数据后，将记录字节数并以 XML 输出方式显示出来。  
  
## <a name="adding-the-target-to-a-session"></a>将目标添加到会话  
 若要将直方图目标添加到扩展事件会话，在创建或更改事件会话时，您必须根据所需目标类型包括下面任一语句：  
  
```  
ADD TARGET package0.histogram  
```  
  
 可以使用 SET 语句设置各种选项。 下面的示例演示了直方图目标的添加方式，将在该目标中收集 sqlserver.checkpoint_end 事件的数据。  
  
```  
ADD TARGET package0.histogram  
(SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id')  
```  
  
 有关详细信息，请参阅[查找具有最多锁定的对象](../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)和[使用扩展事件监视系统活动](../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)。  
  
## <a name="reviewing-the-target-output"></a>查看目标输出  
 直方图目标将数据以 XML 格式序列化到一个调用程序或过程中。 目标输出不遵从任何架构。  
  
 若要查看直方图目标的输出，你可以使用下面的查询，并将 *session_name* 替换为事件会话的名称。  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 以下示例演示了直方图目标的输出格式。  
  
```  
<Slots truncated = "0" buckets=[count]>  
    <Slot count=[count] trunc=[truncated bytes]>  
        <value>  
        </value>  
    </Slot>  
</Slots>  
```  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 扩展事件目标](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
