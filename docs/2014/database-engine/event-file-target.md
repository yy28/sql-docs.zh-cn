---
title: 事件文件目标 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- event file target
- file target [SQL Server extended events]
- targets [SQL Server extended events], file target
ms.assetid: 4f0ee6ec-a0a8-4c38-aa61-8293ab6ac7fd
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4ea74f0361d5152ade31a91424d594d376e513f8
ms.sourcegitcommit: b5cea9c67c7f896944065f09dace17b4929a34f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2018
ms.locfileid: "52267892"
---
# <a name="event-file-target"></a>Event File Target
  事件文件目标是可将完整的缓冲区写入磁盘的目标。  
  
 下表描述了配置事件文件目标时可用的选项。  
  
|选项|允许的值|Description|  
|------------|--------------------|-----------------|  
|filename|任何不超过 260 个字符的字符串。 此值是必需的。|文件位置和文件名。<br /><br /> 可以使用任何文件扩展名。|  
|max_file_size|任何 64 位的整数。 该值是可选的。|文件的最大大小 (MB)。 如果未指定 max_file_size，则文件将一直增长到磁盘变满为止。 默认文件大小为 1GB。<br /><br /> max_file_size 必须大于会话缓冲区的当前大小。 否则，文件目标将无法初始化，并报告 max_file_size 无效。 若要查看缓冲区的当前大小，请查询 [sys.dm_xe_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql) 动态管理视图中的 buffer_size 列。<br /><br /> 如果默认文件大小小于会话缓冲区大小，建议将 max_file_size 设置为 [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) 目录视图中的 max_memory 列中指定的值。<br /><br /> 将 max_file_size 的大小设置为大于会话缓冲区大小时，它可能会向下舍入到最近的会话缓冲区大小的倍数。 这样所产生的目标文件的大小可能小于指定值 max_file_size。 例如，如果缓冲区大小为 100MB 并且 max_file_size 设置为 150MB，则因为在剩余的 50MB 空间中无法放下第二个缓冲区，生成的文件的大小会向下舍入到 100MB。<br /><br /> 如果默认文件大小小于会话缓冲区大小，建议将 max_file_size 设置为 [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) 目录视图中的 max_memory 列中的值。|  
|max_rollover_files|任何 32 位的整数。 该值是可选的。|文件系统中可保留的最多文件数。 默认值为 5。|  
|increment|任何 32 位的整数。 该值是可选的。|文件的增量 (MB)。 如果未指定，则增量的默认值为会话缓冲区大小的两倍。|  
  
 第一次创建事件文件目标时，会在指定的文件名后面附加 _0\_ 以及一个长整型值。 整数值的计算如下 1601 年 1 月 1 日之间的毫秒数的日期和时间创建文件。 后续的回滚文件也将使用此格式。 通过检查该长整型值，可以确定最新的文件。 以下示例演示了文件的命名方式。在该方案中，将文件名选项指定为 C:\OutputFiles\MyOutput.xel：  
  
-   创建的第一个文件 - C:\OutputFiles\MyOutput_0_128500310259380000.xel  
  
-   第一个滚动更新文件 - C:\OutputFiles\MyOutput_0_128505831770890000.xel  
  
-   第二个滚动更新文件 - C:\OutputFiles\MyOutput_0_132410772966237000.xel  
  
## <a name="adding-the-target-to-a-session"></a>将目标添加到会话  
 若要将事件文件目标添加到扩展事件会话，在创建或更改事件会话时，应包括下面的语句，并将 *file_name* 替换为所需的文件名和路径：  
  
```  
ADD TARGET package0.event_file(  
   SET filename='file_name.xel')  
```  
  
## <a name="reviewing-the-target-output"></a>查看目标输出  
 若要查看文件目标的输出，必须使用 sys.fn_xe_file_target_read_file 功能。 建议您将数据转换为 XML。 你可以使用下面的语法，并将 *file_name* 替换为在添加目标时指定的文件名和路径：  
  
```  
SELECT *, CAST(event_data AS XML) AS 'event_data_XML'  
FROM sys.fn_xe_file_target_read_file('file_name*.xel', NULL, NULL, NULL)  
```  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 扩展事件目标](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.fn_xe_file_target_read_file &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql)   
 [CREATE EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
