---
title: "查找具有最多锁定的对象 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
  - "xevents"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "对象 [SQL Server], 扩展事件"
  - "xe"
  - "扩展事件 [SQL Server], 锁"
  - "对象 [SQL Server], 锁"
ms.assetid: fcbadbda-c91c-43f0-a1b5-601e40110e07
caps.latest.revision: 15
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 15
---
# 查找具有最多锁定的对象
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  数据库管理员通常需要识别影响数据库性能的锁定来源。  
  
 例如，可以监视生产服务器是否存在任何可能的瓶颈。 您怀疑可能存在高度争用的资源，并希望了解这些对象占用多少锁定。 一旦识别锁定频率最高的对象，便可采取一些措施来优化对争用对象的访问。  
  
 为此，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的查询编辑器。  
  
### 查找占用最多锁定的对象  
  
1.  在查询编辑器中发出以下语句：  
  
    ```  
    -- Find objects in a particular database that have the most  
    -- lock acquired. This sample uses AdventureWorksDW2012.  
    -- Create the session and add an event and target.  
    --   
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='LockCounts')  
    DROP EVENT session LockCounts ON SERVER  
    GO  
    DECLARE @dbid int  
  
    SELECT @dbid = db_id('AdventureWorksDW2012')  
  
    DECLARE @sql nvarchar(1024)  
    SET @sql = '  
    CREATE event session LockCounts ON SERVER  
    ADD EVENT sqlserver.lock_acquired (WHERE database_id =' + CAST(@dbid AS nvarchar) +')  
    ADD TARGET package0.histogram(   
    SET filtering_event_name=''sqlserver.lock_acquired'', source_type=0, source=''resource_0'')'  
  
    EXEC (@sql)  
    GO  
    ALTER EVENT session LockCounts ON SERVER   
    STATE=start  
    GO  
    --   
    -- Create a simple workload that takes locks.  
    --   
    USE AdventureWorksDW2012  
    GO  
    SELECT TOP 1 * FROM dbo.vAssocSeqLineItems  
    GO  
    -- The histogram target output is available from the   
    -- sys.dm_xe_session_targets dynamic management view in  
    -- XML format.  
    -- The following query joins the bucketizing target output with  
    -- sys.objects to obtain the object names.  
    --  
    SELECT name, object_id, lock_count FROM   
    (SELECT objstats.value('.','bigint') AS lobject_id,   
    objstats.value('@count', 'bigint') AS lock_count  
    FROM (  
    SELECT CAST(xest.target_data AS XML)  
    LockData  
    FROM sys.dm_xe_session_targets xest  
    JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
    JOIN sys.server_event_sessions ses ON xes.name = ses.name  
    WHERE xest.target_name = 'histogram' AND xes.name = 'LockCounts'  
    ) Locks  
    CROSS APPLY LockData.nodes('//HistogramTarget/Slot') AS T(objstats)  
     ) LockedObjects   
    INNER JOIN sys.objects o  
    ON LockedObjects.lobject_id = o.object_id  
    WHERE o.type != 'S' AND o.type = 'U'  
    ORDER BY lock_count desc  
    GO  
    --   
    -- Stop the event session.  
    --   
    ALTER EVENT SESSION LockCounts ON SERVER  
    state=stop  
    GO  
  
    ```  
  
 此过程中的语句完成后，查询编辑器的 **“结果”** 选项卡将显示以下列：  
  
-   name  
  
-   object_id  
  
-   lock_count  
  
## 另请参阅  
 [CREATE EVENT SESSION (Transact-SQL)](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION (Transact-SQL)](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [sys.dm_xe_session_targets (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)   
 [sys.dm_xe_sessions (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)   
 [sys.server_event_sessions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)  
  
  