---
title: JDBC 驱动程序的预处理语句元数据缓存 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97224f53bb716abe3b79dd00df12d0eed4a63cec
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027842"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC 驱动程序的预处理语句元数据缓存
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文介绍了实现的两个更改, 以提高驱动程序的性能。

## <a name="batching-of-unprepare-for-prepared-statements"></a>预定义的语句的 unprepare 批处理
自6.1.6 版本开始, 通过将服务器往返行程降到 SQL Server 来实现性能改进。 以前, 对于每个 prepareStatement 查询, 还会发送对 unprepare 的调用。 现在, 驱动程序正在批处理 unprepare 查询, 直到达到阈值 "ServerPreparedStatementDiscardThreshold", 其默认值为10。

> [!NOTE]  
>  用户可以通过以下方法更改默认值: setServerPreparedStatementDiscardThreshold (int 值)

6\.1.6 中引入的另一项更改是, 在此之前, 驱动程序将始终调用 sp_prepexec。 现在, 在首次执行预定义语句时, 驱动程序会调用 sp_executesql, 对于其余的语句, 它将执行 sp_prepexec 并为其分配一个句柄。 可在[此处](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)找到更多详细信息。

> [!NOTE]  
>  通过使用以下方法将 enablePrepareOnFirstPreparedStatementCall 设置为**true** , 用户可以将默认行为更改为以前版本的始终调用 Sp_prepexec: setEnablePrepareOnFirstPreparedStatementCall (布尔值)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>此更改引入的新 Api 的列表, 用于 unprepare 的预定义语句的批处理

 **SQLServerConnection**
 
|新方法|描述|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|返回当前未完成的已准备语句 unprepare 操作的数目。|
|void closeUnreferencedPreparedStatementHandles()|强制对要执行的任何未完成的已放弃预定义语句执行 unprepare 请求。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|返回特定连接实例的行为。 如果为 false, 则第一次执行将调用 sp_executesql 而不准备语句, 在第二次执行时, 它会调用 sp_prepexec, 并实际设置预定义的语句句柄。 以下执行将调用 sp_execute。 如果语句只执行一次, 则这就不再需要 sp_unprepare 的预定义语句。 可以通过调用 setDefaultEnablePrepareOnFirstPreparedStatementCall () 来更改此选项的默认值。|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|指定特定连接实例的行为。 如果值为 false, 则第一次执行将调用 sp_executesql 而不是 prepare 语句, 在第二次执行时, 它会调用 sp_prepexec, 并实际设置预定义的语句句柄。 以下执行将调用 sp_execute。 如果语句只执行一次, 则这就不再需要 sp_unprepare 的预定义语句。|
|int getServerPreparedStatementDiscardThreshold()|返回特定连接实例的行为。 此设置控制在执行在服务器上清除未完成的句柄之前, 每个连接可以完成多少个未完成的已准备语句放弃操作 (sp_unprepare)。 如果设置为 < = 1, 则在预定义的语句关闭时将立即执行 unprepare 操作。 如果将其设置为 {@literal >} 1, 则这些调用将一起分批, 以避免调用 sp_unprepare 的开销过于频繁。 可以通过调用 getDefaultServerPreparedStatementDiscardThreshold () 来更改此选项的默认值。|
|void setServerPreparedStatementDiscardThreshold(int value)|指定特定连接实例的行为。 此设置控制在执行在服务器上清除未完成的句柄之前, 每个连接可以完成多少个未完成的已准备语句放弃操作 (sp_unprepare)。 如果设置为 < = 1, 则在预定义的语句关闭时立即执行 unprepare 操作。 如果将其设置为 > 1, 则这些调用将一起分批, 以避免调用 sp_unprepare 的开销过于频繁。|

 **SQLServerDataSource**
 
|新方法|描述|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|如果此配置为 false, 则第一次执行预定义语句时, 将调用 sp_executesql 而不准备语句, 在第二次执行时, 它会调用 sp_prepexec 并实际设置预定义的语句句柄。 以下执行将调用 sp_execute。 如果语句只执行一次, 则这就不再需要 sp_unprepare 的预定义语句。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|如果此配置返回 false, 则第一次执行预定义语句时将调用 sp_executesql 而不准备语句, 在第二次执行执行后, 它将调用 sp_prepexec 并实际设置预定义的语句句柄。 以下执行将调用 sp_execute。 如果语句只执行一次, 则这就不再需要 sp_unprepare 的预定义语句。|
|void setServerPreparedStatementDiscardThreshold (int serverPreparedStatementDiscardThreshold)|此设置控制在执行在服务器上清除未完成的句柄之前, 每个连接可以完成多少个未完成的已准备语句放弃操作 (sp_unprepare)。 如果设置为 < = 1, 则在预定义的语句关闭时立即执行 unprepare 操作。 如果将其设置为 {@literal >} 1, 则这些调用将一起分批, 以避免调用 sp_unprepare 过于频繁的开销|
|int getServerPreparedStatementDiscardThreshold()|此设置控制在执行在服务器上清除未完成的句柄之前, 每个连接可以完成多少个未完成的已准备语句放弃操作 (sp_unprepare)。 如果设置为 < = 1, 则在预定义的语句关闭时立即执行 unprepare 操作。 如果将其设置为 {@literal >} 1, 则这些调用将一起分批, 以避免调用 sp_unprepare 的开销过于频繁。|

## <a name="prepared-statement-metatada-caching"></a>预定义的语句元数据缓存
从 6.3.0-预览版本, Microsoft JDBC driver for SQL Server 支持预定义的语句缓存。 在 v 6.3.0-preview 之前, 如果一个查询执行已准备好并存储在缓存中的查询, 则再次调用相同的查询将不会导致进行准备。 现在, 驱动程序会在缓存中查找查询, 并查找句柄并通过 sp_execute 执行它。
默认情况下,**已禁用**预定义的语句元数据缓存。 若要启用它, 需要对连接对象调用以下方法:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

例如：`connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>此更改引入的新 Api 的列表, 用于预定义的语句元数据缓存

 **SQLServerConnection**
 
|新方法|描述|  
|-----------|-----------------|  
|void setDisableStatementPooling (布尔值)|将语句池设置为 true 或 false。|
|boolean getDisableStatementPooling()|如果禁用了语句池, 则返回 true。|
|void setStatementPoolingCacheSize(int value)|指定此连接的预定义语句缓存大小。 如果值小于 1, 则表示没有缓存。|
|int getStatementPoolingCacheSize()|返回此连接的预定义语句缓存大小。 如果值小于 1, 则表示没有缓存。|
|int getStatementHandleCacheEntryCount()|返回当前汇集的已准备语句句柄的数目。|
|boolean isPreparedStatementCachingEnabled()|此连接是否启用了语句池。|

 **SQLServerDataSource**
 
|新方法|描述|  
|-----------|-----------------|  
|void setDisableStatementPooling (布尔值 disableStatementPooling)|将该语句池设置为 true 或 false|
|boolean getDisableStatementPooling()|如果禁用了语句池, 则返回 true。|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|指定此连接的预定义语句缓存大小。 如果值小于 1, 则表示没有缓存。|
|int getStatementPoolingCacheSize()|返回此连接的预定义语句缓存大小。 如果值小于 1, 则表示没有缓存。|

## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序提升性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
