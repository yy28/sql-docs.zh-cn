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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027842"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC 驱动程序的预处理语句元数据缓存
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文介绍了为提高驱动程序的性能而实现的两个更改。

## <a name="batching-of-unprepare-for-prepared-statements"></a>预定义语句的 unprepare 批处理
自 6.1.6 预览版开始，通过将服务器往返行程最小化到 SQL Server 来实现性能改进。 此前，对于每个 prepareStatement 查询，还会发送对 unprepare 的调用。 现在，驱动程序将批处理 unprepare 查询，直到达到阈值“ServerPreparedStatementDiscardThreshold”，其默认值为 10。

> [!NOTE]  
>  用户可以通过以下方法更改默认值：setServerPreparedStatementDiscardThreshold(int value)

6\.1.6 预览版中引入的另一个更改是在此之前，驱动程序将始终调用 sp_prepexec。 现在，在第一次执行预定义语句时，驱动程序将调用 sp_executesql，对于其他情况，则执行 sp_prepexec 并为其分配一个句柄。 [此处](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)提供了更多详细信息。

> [!NOTE]  
>  通过使用以下方法将 enablePrepareOnFirstPreparedStatementCall 设置为 true  ，用户可以将默认行为更改为先前版本的“始终调用 sp_prepexec”：setEnablePrepareOnFirstPreparedStatementCall(boolean value)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>此更改引入了新 API 列表，用于对预定义语句进行 unprepare 批处理

 **SQLServerConnection**
 
|新方法|说明|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|返回当前未完成的预定义语句的 unprepare 操作数。|
|void closeUnreferencedPreparedStatementHandles()|对任何未完成的已放弃预定义语句强制执行 unprepare 请求。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|返回特定连接实例的行为。 如果为 false，则第一次执行将调用 sp_executesql 而不是预定义语句，发生第二次执行后，它随即调用 sp_prepexec 并实际设置一个预定义语句句柄。 以下执行将调用 sp_execute。 如果该语句仅执行一次，则无需在预定义语句关闭时使用 sp_unprepare。 可以通过调用 setDefaultEnablePrepareOnFirstPreparedStatementCall() 来更改此选项的默认值。|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|指定特定连接实例的行为。 如果值为 false，则第一次执行将调用 sp_executesql 而不是预定义语句，发生第二次执行后，它随即调用 sp_prepexec 并实际设置一个预定义语句句柄。 以下执行将调用 sp_execute。 如果该语句仅执行一次，则无需在预定义语句关闭时使用 sp_unprepare。|
|int getServerPreparedStatementDiscardThreshold()|返回特定连接实例的行为。 此设置控制在执行调用以清除服务器上未完成的句柄之前，每个连接可以有多少个未完成的预定义语句放弃操作 (sp_unprepare) 处于未处理状态。 如果设置 <= 1，则在预定义语句关闭时将立即执行 unprepare 操作。 如果设置为 {@literal >} 1，则会对这些调用进行批处理，以避免过于频繁地调用 sp_unprepare 的开销。 可以通过调用 getDefaultServerPreparedStatementDiscardThreshold() 来更改此选项的默认值。|
|void setServerPreparedStatementDiscardThreshold(int value)|指定特定连接实例的行为。 此设置控制在执行调用以清除服务器上未完成的句柄之前，每个连接可以有多少个未完成的预定义语句放弃操作 (sp_unprepare) 处于未处理状态。 如果设置 <= 1，则在预定义语句关闭时将立即执行 unprepare 操作。 如果设置为 > 1，则会对这些调用进行批处理，以避免过于频繁地调用 sp_unprepare 的开销。|

 **SQLServerDataSource**
 
|新方法|说明|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|如果此配置为 false，则第一次执行预定义语句时，将调用 sp_executesql 而不是预定义语句，发生第二次执行后，它随即调用 sp_prepexec 并实际设置一个预定义语句句柄。 以下执行将调用 sp_execute。 如果该语句仅执行一次，则无需在预定义语句关闭时使用 sp_unprepare。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|如果此配置返回 false，则第一次执行预定义语句时，将调用 sp_executesql 而不是预定义语句，发生第二次执行后，它随即调用 sp_prepexec 并实际设置一个预定义语句句柄。 以下执行将调用 sp_execute。 如果该语句仅执行一次，则无需在预定义语句关闭时使用 sp_unprepare。|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|此设置控制在执行调用以清除服务器上未完成的句柄之前，每个连接可以有多少个未完成的预定义语句放弃操作 (sp_unprepare) 处于未处理状态。 如果设置 <= 1，则在预定义语句关闭时将立即执行 unprepare 操作。 如果设置为 {@literal >} 1，则会对这些调用进行批处理，以避免过于频繁地调用 sp_unprepare 的开销|
|int getServerPreparedStatementDiscardThreshold()|此设置控制在执行调用以清除服务器上未完成的句柄之前，每个连接可以有多少个未完成的预定义语句放弃操作 (sp_unprepare) 处于未处理状态。 如果设置 <= 1，则在预定义语句关闭时将立即执行 unprepare 操作。 如果设置为 {@literal >} 1，则会对这些调用进行批处理，以避免过于频繁地调用 sp_unprepare 的开销。|

## <a name="prepared-statement-metatada-caching"></a>预定义语句元数据缓存
从 6.3.0 预览版开始，Microsoft JDBC driver for SQL Server 将支持预定义语句缓存。 在 v6.3.0 预览版之前，如果某个用户执行已预定义并存储在缓存中的查询，那么再次调用相同的查询将不会导致预定义工作。 现在，驱动程序会在缓存中查找查询并查找句柄，然后通过 sp_execute 来执行查询。
默认情况下，预定义语句元数据缓存处于“禁用”  状态。 若要启用它，需要对连接对象调用以下方法：

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

例如：`connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>此更改引入了新 API 列表，用于预定义语句的元数据缓存

 **SQLServerConnection**
 
|新方法|说明|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|将语句池设置为 true 或 false。|
|boolean getDisableStatementPooling()|如果禁用了语句池，则返回 true。|
|void setStatementPoolingCacheSize(int value)|指定此连接的预定义语句缓存的大小。 如果值小于 1，则表示没有缓存。|
|int getStatementPoolingCacheSize()|返回此连接的预定义语句缓存的大小。 如果值小于 1，则表示没有缓存。|
|int getStatementHandleCacheEntryCount()|返回当前已入池的预定义语句句柄的数目。|
|boolean isPreparedStatementCachingEnabled()|是否为此连接启用语句池。|

 **SQLServerDataSource**
 
|新方法|说明|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|将语句池设置为 true 或 false|
|boolean getDisableStatementPooling()|如果禁用了语句池，则返回 true。|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|指定此连接的预定义语句缓存的大小。 如果值小于 1，则表示没有缓存。|
|int getStatementPoolingCacheSize()|返回此连接的预定义语句缓存的大小。 如果值小于 1，则表示没有缓存。|

## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序提升性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
