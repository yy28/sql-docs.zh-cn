---
title: JDBC 驱动程序的预处理语句元数据缓存 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c412a4364e18a70cf10d9896138c5056318ae20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767333"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC 驱动程序的预处理语句元数据缓存
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文介绍的两个更改的实现来增强的驱动程序的性能。

## <a name="batching-of-unprepare-for-prepared-statements"></a>为预定义语句的批处理 Unprepare
由于版本 6.1.6-preview 中的性能改进实现通过最大程度减少服务器往返到 SQL Server 的通信。 以前，对于每个 prepareStatement 查询，若要撤消的调用还会发送。 现在，批处理驱动程序未准备查询最多阈值"ServerPreparedStatementDiscardThreshold"，具有默认值为 10。

> [!NOTE]  
>  用户可以使用以下方法更改默认值： setServerPreparedStatementDiscardThreshold （int 值）

从 6.1.6-preview 引入了一个更改是，在此之前，驱动程序将始终调用 sp_prepexec。 现在，已准备的语句的第一次执行，驱动程序调用 sp_executesql，其余部分，它执行 sp_prepexec 并为其分配一个句柄。 可以找到更多详细信息[此处](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)。

> [!NOTE]  
>  用户可以更改默认行为与以前版本的始终调用设置 enablePrepareOnFirstPreparedStatementCall 到 sp_prepexec **，则返回 true**使用以下方法：setEnablePrepareOnFirstPreparedStatementCall （布尔值）

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>为预定义语句的未准备进行此更改后，进行批处理的引入的新 Api 的列表

 **SQLServerConnection**
 
|新方法|描述|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|返回当前未处理的已准备语句撤消操作。|
|void closeUnreferencedPreparedStatementHandles()|强制之请求的任何未完成丢弃准备的语句执行。|
|布尔 getEnablePrepareOnFirstPreparedStatementCall()|返回特定的连接实例的行为。 如果为 false 则调用 sp_executesql 后第二次执行发生调用 sp_prepexec 未准备语句，第一次执行和将其实际安装程序已准备的语句句柄。 以下执行调用 sp_execute。 如果该语句仅执行一次，这关闭使 sp_unprepare 已准备的语句上的需要。 可以通过调用 setDefaultEnablePrepareOnFirstPreparedStatementCall() 更改此选项的默认值。|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|指定特定的连接实例的行为。 如果值为 false 则调用 sp_executesql 后第二次执行发生调用 sp_prepexec 未准备语句，第一次执行和将其实际安装程序已准备的语句句柄。 以下执行调用 sp_execute。 如果该语句仅执行一次，这关闭使 sp_unprepare 已准备的语句上的需要。|
|int getServerPreparedStatementDiscardThreshold()|返回特定的连接实例的行为。 此设置控制多少未完成准备语句丢弃之前执行调用以清理服务器上未完成的句柄，则可以每个连接未完成操作 (sp_unprepare)。 如果设置为 < = 1，撤消已准备的语句关闭上立即执行操作。 如果设置为 {@literal >} 1，这些调用会放在一起以避免过于频繁调用 sp_unprepare 的开销。 可以通过调用 getDefaultServerPreparedStatementDiscardThreshold() 更改此选项的默认值。|
|void setServerPreparedStatementDiscardThreshold(int value)|指定特定的连接实例的行为。 此设置控制多少未完成准备语句丢弃之前执行调用以清理服务器上未完成的句柄，则可以每个连接未完成操作 (sp_unprepare)。 如果设置为 < = 1 撤消操作已准备的语句关闭上立即执行。 如果设置为 > 1 这些调用会一起批处理，以避免过于频繁调用 sp_unprepare 的开销。|

 **SQLServerDataSource**
 
|新方法|描述|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|如果此配置为 false 首次执行的已准备的语句调用 sp_executesql 和未准备语句后第二次执行发生调用 sp_prepexec 和实际安装程序已准备的语句句柄。 以下执行调用 sp_execute。 如果该语句仅执行一次，这关闭使 sp_unprepare 已准备的语句上的需要。|
|布尔 getEnablePrepareOnFirstPreparedStatementCall()|如果此配置返回 false 首次执行的已准备的语句调用 sp_executesql，并且不准备语句，第二次执行发生后，它调用 sp_prepexec 并实际安装程序已准备的语句句柄。 以下执行调用 sp_execute。 如果该语句仅执行一次，这关闭使 sp_unprepare 已准备的语句上的需要。|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|此设置控制多少未完成准备语句丢弃之前执行调用以清理服务器上未完成的句柄，则可以每个连接未完成操作 (sp_unprepare)。 如果设置为 < = 1 撤消操作已准备的语句关闭上立即执行。 如果设置为 {@literal >} 1 这些调用会一起批处理，以避免过于频繁调用 sp_unprepare 的开销|
|int getServerPreparedStatementDiscardThreshold()|此设置控制多少未完成准备语句丢弃之前执行调用以清理服务器上未完成的句柄，则可以每个连接未完成操作 (sp_unprepare)。 如果设置为 < = 1 撤消操作已准备的语句关闭上立即执行。 如果设置为 {@literal >} 1 这些调用会一起批处理，以避免过于频繁调用 sp_unprepare 的开销。|

## <a name="prepared-statement-metatada-caching"></a>已准备语句元数据缓存
从 6.3.0-preview 版本，适用于 SQL Server 的 Microsoft JDBC 驱动程序支持缓存已准备的语句。 之前 v6.3.0-preview，如果其中一个执行的查询的已准备好并存储在缓存中，再次调用相同的查询不会导致做好准备。 现在，该驱动程序查找缓存中的查询和查找的句柄并执行与 sp_execute。
已准备语句元数据缓存**禁用**默认情况下。 若要启用它，需要在连接对象上调用以下方法：

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

例如：`connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>进行此更改后，为已准备的语句引入的新 Api 列表元数据缓存

 **SQLServerConnection**
 
|新方法|描述|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|设置为 true 或 false 的语句池。|
|布尔 getDisableStatementPooling()|如果禁用语句池，则返回 true。|
|void setStatementPoolingCacheSize(int value)|指定用于此连接的已准备的语句缓存的大小。 值小于 1 表示没有缓存。|
|int getStatementPoolingCacheSize()|返回此连接的已准备的语句缓存的大小。 值小于 1 表示没有缓存。|
|int getStatementHandleCacheEntryCount()|返回当前的共用预定义的语句句柄数。|
|布尔 isPreparedStatementCachingEnabled()|是否启用语句池或不适用于此连接。|

 **SQLServerDataSource**
 
|新方法|描述|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|设置池的语句为 true 或 false|
|布尔 getDisableStatementPooling()|如果禁用语句池，则返回 true。|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|指定用于此连接的已准备的语句缓存的大小。 值小于 1 表示没有缓存。|
|int getStatementPoolingCacheSize()|返回此连接的已准备的语句缓存的大小。 值小于 1 表示没有缓存。|

## <a name="see-also"></a>另请参阅  
 [借助 JDBC 驱动程序提高性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
