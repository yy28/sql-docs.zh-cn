---
title: 准备语句的元数据缓存 JDBC 驱动程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eb093c9102cbafde8e43fc69f2860831634bfee5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>已准备的语句的元数据缓存 JDBC 驱动程序
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文提供有关实现的目的是提高驱动程序的性能的两个更改的信息。

## <a name="batching-of-unprepare-for-prepared-statements"></a>对于已准备的语句的批处理 Unprepare
由于版本 6.1.6-preview 中的性能改进已实现通过最小化服务器舍入到 SQL Server 的过程。 以前，对于每个 prepareStatement 查询，还发送的已准备的调用。 现在，批处理驱动程序 unprepare 查询最多阈值"ServerPreparedStatementDiscardThreshold"，具有默认值为 10。

> [!NOTE]  
>  用户可以使用以下方法更改默认值： setServerPreparedStatementDiscardThreshold （int 值）

从 6.1.6-preview 引入的一次详细更改是在此之前，驱动程序将始终调用 sp_prepexec。 现在，第一个执行的已准备的语句，驱动程序将调用 sp_executesql 和其余它将执行 sp_prepexec 并为其指定句柄。 找不到更多详细信息[此处](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)。

> [!NOTE]  
>  用户可以更改默认行为与以前版本的始终调用设置 enablePrepareOnFirstPreparedStatementCall 到 sp_prepexec **true**使用以下方法：setEnablePrepareOnFirstPreparedStatementCall （布尔值）

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>进行此更改后，批处理的引入的新 Api 的列表 Unprepare 对的已准备的语句

 **SQLServerConnection**
 
|新方法|Description|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|返回的数目当前未完成已准备语句撤消操作。|
|void closeUnreferencedPreparedStatementHandles()|强制任何未完成丢弃已准备语句得以执行 unprepare 请求。|
|布尔 getEnablePrepareOnFirstPreparedStatementCall()|返回的特定连接实例的行为。 如果为 false 则调用 sp_executesql 后会发生第二次执行情况它调用 sp_prepexec 做好准备的语句，在首次执行和将其实际安装程序已准备的语句句柄。 以下执行调用 sp_execute。 如果仅一次执行的语句，这关闭缓解 sp_unprepare 已准备的语句上的需要。 可以通过调用 setDefaultEnablePrepareOnFirstPreparedStatementCall() 更改此选项的默认值。|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|指定的特定连接实例的行为。 如果值为 false 则调用 sp_executesql 后会发生第二次执行情况它调用 sp_prepexec 做好准备的语句，在首次执行和将其实际安装程序已准备的语句句柄。 以下执行调用 sp_execute。 如果仅一次执行的语句，这关闭缓解 sp_unprepare 已准备的语句上的需要。|
|int getServerPreparedStatementDiscardThreshold()|返回的特定连接实例的行为。 此设置控制多少未完成准备语句放弃操作 (sp_unprepare) 可以是每个连接未完成之前执行的调用，以清理服务器上未完成的句柄。 如果设置为 < = 1，unprepare 在关闭已准备的语句上立即执行操作。 如果设置为 {@literal >} 1，这些调用进行批处理在一起以避免调用 sp_unprepare 开销过于频繁。 可以通过调用 getDefaultServerPreparedStatementDiscardThreshold() 更改此选项的默认值。|
|void setServerPreparedStatementDiscardThreshold(int value)|指定的特定连接实例的行为。 此设置控制多少未完成准备语句放弃操作 (sp_unprepare) 可以是每个连接未完成之前执行的调用，以清理服务器上未完成的句柄。 如果设置为 < = 1 unprepare 操作在关闭已准备的语句上立即执行。 如果设置为 > 1 进行一起批处理这些调用以避免调用 sp_unprepare 过于频繁的开销。|

 **SQLServerDataSource**
 
|新方法|Description|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|如果此配置为 false 则调用 sp_executesql 后会发生第二次执行情况它调用 sp_prepexec 做好准备的语句，在首次执行的已准备的语句和将其实际安装程序已准备的语句句柄。 以下执行调用 sp_execute。 如果仅一次执行的语句，这关闭缓解 sp_unprepare 已准备的语句上的需要。|
|布尔 getEnablePrepareOnFirstPreparedStatementCall()|如果此配置返回 false 已准备的语句在首次执行调用 sp_executesql，并且不准备一条语句，第二次执行发生后，它将调用 sp_prepexec 和实际安装程序已准备的语句句柄。 以下执行调用 sp_execute。 如果仅一次执行的语句，这关闭缓解 sp_unprepare 已准备的语句上的需要。|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|此设置控制多少未完成准备语句放弃操作 (sp_unprepare) 可以是每个连接未完成之前执行的调用，以清理服务器上未完成的句柄。 如果设置为 < = 1 unprepare 操作在关闭已准备的语句上立即执行。 如果设置为 {@literal >} 这些调用进行一起批处理来避免开销的过于频繁调用 sp_unprepare 1|
|int getServerPreparedStatementDiscardThreshold()|此设置控制多少未完成准备语句放弃操作 (sp_unprepare) 可以是每个连接未完成之前执行的调用，以清理服务器上未完成的句柄。 如果设置为 < = 1 unprepare 操作在关闭已准备的语句上立即执行。 如果设置为 {@literal >} 1 这些调用进行一起批处理，以避免调用 sp_unprepare 过于频繁的开销。|

## <a name="prepared-statement-metatada-caching"></a>已准备语句元数据缓存
6.3.0-preview 从版开始，Microsoft JDBC driver for SQL Server 支持已准备的语句缓存。 之前 v6.3.0-预览版中，如果其中一个执行的查询已准备并存储在缓存中，再次调用相同的查询不会导致做好准备。 现在，该驱动程序查找缓存中的查询和查找的句柄并使用 sp_execute 执行它。
已准备语句元数据缓存是**禁用**默认情况下。 若要启用它，你需要在连接对象上调用以下方法：

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

例如： `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>进行此更改后，为已准备的语句引入的新 Api 的列表元数据缓存

 **SQLServerConnection**
 
|新方法|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|设置为 true 或 false 池语句。|
|布尔 getDisableStatementPooling()|如果禁用语句池，则返回 true。|
|void setStatementPoolingCacheSize(int value)|指定此连接的已准备的语句缓存的大小。 小于 1 的值意味着没有缓存。|
|int getStatementPoolingCacheSize()|返回此连接的已准备的语句缓存的大小。 小于 1 的值意味着没有缓存。|
|int getStatementHandleCacheEntryCount()|返回当前的共用已准备的语句句柄数。|
|布尔 isPreparedStatementCachingEnabled()|是否启用语句池或不适用于此连接。|

 **SQLServerDataSource**
 
|新方法|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|设置池的语句为 true 或 false|
|布尔 getDisableStatementPooling()|如果禁用语句池，则返回 true。|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|指定此连接的已准备的语句缓存的大小。 小于 1 的值意味着没有缓存。|
|int getStatementPoolingCacheSize()|返回此连接的已准备的语句缓存的大小。 小于 1 的值意味着没有缓存。|

## <a name="see-also"></a>另请参阅  
 [借助 JDBC 驱动程序提高性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
