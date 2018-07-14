---
title: 创建扩展的事件会话使用查询编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- create extended events session
- extended events [SQL Server], create session
ms.assetid: cba0e02b-b201-4863-bf1b-9164e68e5fa8
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8524274c0fe1f79bb0f62008ba0caf6ad115004b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37207697"
---
# <a name="create-an-extended-events-session-using-query-editor"></a>使用查询编辑器创建扩展事件会话
  您可以使用查询编辑器创建扩展事件会话，也可以在对象资源管理器中创建会话。 在对象资源管理器中，扩展事件提供了两个可用来创建、修改和查看事件会话数据的用户界面，即，一个指导您完成事件会话创建过程的向导和一个提供了更多高级配置选项的新会话 UI。 您可以创建扩展事件会话来诊断 SQL Server 跟踪，这样您便能解决如下问题：  
  
-   查找最消耗资源的查询  
  
-   查找导致闩锁争用的根本原因  
  
-   查找阻止其他查询的查询  
  
-   解决因重新编译查询导致的 CPU 使用率过高的问题  
  
-   排除死锁故障  
  
 有关如何使用新建会话向导创建扩展事件会话的信息，请参阅[使用向导（对象资源管理器）创建扩展事件会话](../ssms/object/object-explorer.md)。 有关如何使用新建会话 UI 创建扩展事件会话的信息，请参阅[使用新建会话创建扩展事件会话](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)。  
  
##  <a name="BeforeYouBegin"></a> 权限  
 若要创建扩展事件会话，您必须具有 ALTER ANY EVENT SESSION 权限。  
  
## <a name="creating-an-extended-events-session-using-query-editor"></a>使用查询编辑器创建扩展事件会话  
  
#### <a name="to-create-an-extended-events-session"></a>创建扩展事件会话  
  
1.  下面的过程说明如何通过使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中的查询编辑器创建扩展事件会话。  
  
     确定要在会话中使用的事件。 若要查看所有可用事件以及关键字和渠道，请使用以下查询：  
  
    > [!NOTE]  
    >  有关关键字和渠道的信息，请参阅 [SQL Server 扩展事件包](../relational-databases/extended-events/sql-server-extended-events-packages.md)。  
  
    ```  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
       (  
       SELECT event_package = o.package_guid, o.description,   
       event=c.object_name, channel = v.map_value  
       FROM sys.dm_xe_objects o  
       LEFT JOIN sys.dm_xe_object_columns c ON o.name = c.object_name  
       INNER JOIN sys.dm_xe_map_values v ON c.type_name = v.name   
       AND c.column_value = cast(v.map_key AS nvarchar)  
       WHERE object_type = 'event' AND (c.name = 'CHANNEL' or c.name IS NULL)  
       ) c LEFT JOIN   
       (  
       SELECT event_package = c.object_package_guid, event = c.object_name,   
       keyword = v.map_value  
       FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
       ON c.type_name = v.name AND c.column_value = v.map_key   
       AND c.type_package_guid = v.object_package_guid  
       INNER JOIN sys.dm_xe_objects o ON o.name = c.object_name   
       AND o.package_guid = c.object_package_guid  
       WHERE object_type = 'event' AND c.name = 'KEYWORD'   
       ) k  
       ON  
       k.event_package = c.event_package AND (k.event=c.event or k.event IS NULL)  
       INNER JOIN sys.dm_xe_packages p ON p.guid = c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
2.  在新的查询窗口中，添加以下语句以便创建一个事件会话，并且使用你要使用的会话名称替换 *session_name* ：  
  
    > [!IMPORTANT]  
    >  此过程的步骤 2 到 6 描述事件会话定义的各部分。 在执行前，您要将所有语句都添加到单个查询窗口中。 有关完整示例，请参阅本主题的“示例”部分。  
  
    ```  
    CREATE EVENT SESSION session_name   
    ON SERVER  
    ```  
  
3.  以 *package_name*.*event_name*格式添加你要监视的事件。 对于每个事件，添加如下的一行：  
  
    ```  
    ADD EVENT package_name.event_name  
    ```  
  
     例如：  
  
    ```  
    ADD EVENT sqlserver.file_read_completed,  
    ADD EVENT sqlserver.file_write_completed  
    ```  
  
4.  （可选）在您添加一个事件后，可以添加要执行的操作。 还可以添加谓词。 谓词用于确立目标何时应使用事件信息的条件。 通过使用 ACTION 子句添加操作，并且通过使用 WHERE 子句添加谓词。 例如，若要添加为 sqlserver.file_read_completed 事件捕获 [!INCLUDE[tsql](../includes/tsql-md.md)] 文本并且文件 ID 等于 1 的操作和谓词，要包括以下语句：  
  
    ```  
    ADD EVENT sqlserver.file_read_completed  
       (ACTION (sqlserver.sql_text)  
       WHERE file_id = 1),  
    ```  
  
    -   若要查看可用的操作，请使用以下查询：  
  
        ```  
        SELECT p.name AS 'package_name', xo.name AS 'action_name', xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'action'  
        AND (xo.capabilities & 1 = 0   
        OR xo.capabilities IS NULL)  
        ORDER BY p.name, xo.name  
        ```  
  
    -   若要查看可用于事件的谓词，请使用以下查询，并且使用你要为其添加谓词的事件名称替换 *event_name* ：  
  
        ```  
        SELECT *  
        FROM sys.dm_xe_object_columns  
        WHERE object_name = 'event_name'  
        AND column_type = 'data'  
        ```  
  
         例如：  
  
        ```  
        SELECT *   
        FROM sys.dm_xe_object_columns   
        WHERE object_name = 'file_read_completed'  
        AND column_type = 'data'  
        ```  
  
         请注意，您还可以添加全局谓词源。 全局谓词源可用于任何谓词表达式中。 若要查看可用的全局谓词源，请使用以下查询：  
  
        ```  
        SELECT p.name AS package_name, xo.name AS predicate_name  
           , xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'pred_source'  
        ORDER BY p.name, xo.name  
        ```  
  
         例如，您可以使用以下谓词表达式以便指定仅为前五次发生的事件收集数据。  
  
        ```  
        WHERE package0.counter <= 5  
        ```  
  
5.  添加将处理和使用事件数据的预期目标。 使用以下格式：  
  
    ```  
    ADD TARGET package_name.target_name  
    ```  
  
     以下示例添加异步文件目标：  
  
    ```  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
    ```  
  
     若要查看可用目标的列表，请使用以下查询：  
  
    ```  
    SELECT p.name AS 'package_name', xo.name AS 'target_name'  
       , xo.description, xo.object_type   
    FROM sys.dm_xe_objects AS xo  
    JOIN sys.dm_xe_packages AS p  
       ON xo.package_guid = p.guid  
    WHERE xo.object_type = 'target'  
    AND (xo.capabilities & 1 = 0  
    OR xo.capabilities IS NULL)  
    ORDER BY p.name, xo.name  
    ```  
  
    > [!NOTE]  
    >  有关不同目标类型的信息，请参阅 [SQL Server 扩展事件目标](../../2014/database-engine/sql-server-extended-events-targets.md)。  
  
6.  查看和添加任何附加的配置选项。 例如，您可以配置不同的选项，例如事件保留模式、事件在内存中缓冲的时间或者在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 启动时事件会话是否应自动启动。 主题 [ALTER EVENT SESSION (Transact SQL)](/sql/t-sql/statements/alter-event-session-transact-sql) 中对这些选项进行了介绍。 请注意，如果未指定这些选项，则分配默认值。  
  
7.  启动会话。  
  
    > [!NOTE]  
    >  有关如何查看会话结果的详细信息，请参阅针对在联机丛书的 [SQL Server 扩展事件目标](../../2014/database-engine/sql-server-extended-events-targets.md) 节点中使用的目标类型的相应主题。  
  
 下面的示例创建名为 IOActivity 的扩展事件会话，该会话捕获以下信息：  
  
-   已完成文件读取的事件数据，包括用于文件 ID 等于 1 的文件读取的关联 [!INCLUDE[tsql](../includes/tsql-md.md)] 文本。  
  
-   已完成文件写入的事件数据。  
  
-   数据从日志缓存写入物理日志文件时的事件数据。  
  
 该会话将输出发送到某一文件目标。  
  
```  
CREATE EVENT SESSION IOActivity  
ON SERVER  
  
ADD EVENT sqlserver.file_read_completed  
   (  
   ACTION (sqlserver.sql_text)  
   WHERE file_id = 1),  
ADD EVENT sqlserver.file_write_completed,  
ADD EVENT sqlserver.databases_log_flush  
  
ADD TARGET package0.asynchronous_file_target   
   (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
```  
  
## <a name="see-also"></a>请参阅  
 [CREATE EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/create-event-session-transact-sql)   
 [SQL Server 扩展事件目标](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [SQL Server 扩展事件包](../relational-databases/extended-events/sql-server-extended-events-packages.md)  
  
  
