---
title: Microsoft OLE DB Provider for Microsoft Jet |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd81c1c5efcb2ca8ebedac756d569ca947aac051
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271616"
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Microsoft OLE DB Provider for Microsoft Jet 概述
用于 Microsoft Jet OLE DB 访问接口允许 ADO 来访问 Microsoft Jet 数据库。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到此提供程序，设置*提供程序*参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性设置为以下：

```
Microsoft.Jet.OLEDB.4.0
```

 读取[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性还将返回此字符串。

## <a name="typical-connection-string"></a>典型的连接字符串
 此提供程序的典型连接字符串是：

```
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 该字符串包含这些关键字：

|关键字|Description|
|-------------|-----------------|
|**提供程序**|指定 Microsoft Jet 的 OLE DB 访问接口。|
|**数据源**|指定数据库路径和文件名 (例如， `c:\Northwind.mdb`)。|
|**用户 ID**|指定的用户名。 如果未指定此关键字，此字符串中，"`admin`"，默认情况下使用。|
|**密码**|指定的用户密码。 如果未指定此关键字，空字符串 ("")，默认情况下使用。|

> [!NOTE]
>  如果你要连接到的数据源提供程序支持 Windows 身份验证，你应指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是用户 ID 和密码连接字符串中的信息。

## <a name="provider-specific-connection-parameters"></a>提供程序特定的连接参数
 用于 Microsoft Jet OLE DB 访问接口支持除由 ADO 定义的多个特定于提供程序的动态属性。 与所有其他**连接**参数，它们可以通过使用设置**属性**集合**连接**对象或作为连接字符串的一部分。

 下表列出了这些属性以及在括号中的相应 OLE DB 属性名称。

|参数|Description|
|---------------|-----------------|
|Jet OLEDB:Compact 回收的空间量 (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|指示空间，以字节为单位，可以通过对数据库进行压缩回收量的估计值。 建立数据库连接后，此值才有效。|
|Jet OLEDB:Connection 控件 (DBPROP_JETOLEDB_CONNECTIONCONTROL)|指示用户是否可以连接到数据库。|
|Jet OLEDB： 创建系统数据库 (DBPROP_JETOLEDB_CREATESYSTEMDATABASE)|指示在创建新的数据源时是否应创建一个系统数据库。|
|Jet OLEDB:Database 锁定模式 (DBPROP_JETOLEDB_DATABASELOCKMODE)|指示此数据库的锁定模式。 若要打开的数据库的第一个用户确定数据库处于打开状态时使用的模式。|
|Jet OLEDB:Database 密码 (DBPROP_JETOLEDB_DATABASEPASSWORD)|指示数据库密码。|
|Jet OLEDB： 未复制压缩 (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE) 上的区域设置|指示压缩数据库时，Jet 是否应该复制区域设置信息。|
|Jet OLEDB： 加密数据库 (DBPROP_JETOLEDB_ENCRYPTDATABASE)|指示是否应加密压缩的数据库。 如果未设置此属性，如果还加密原始数据库将加密压缩的数据库。|
|Jet OLEDB:Engine 类型 (DBPROP_JETOLEDB_ENGINE)|指示用于访问当前数据存储的存储引擎。|
|Jet OLEDB:Exclusive 异步延迟 (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|指示时间，以毫秒为单位，Jet 可能延迟异步写入到磁盘以独占方式打开该数据库的最大长度。<br /><br /> 将忽略此属性，除非**Jet OLEDB:Flush 事务超时**设置为 0。|
|Jet OLEDB:Flush 事务超时 (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|指示存储在缓存中，以便异步写入的数据实际写入之前要等待的时间量到磁盘。 此设置将重写的值**Jet OLEDB： 共享异步延迟**和**Jet OLEDB:Exclusive 异步延迟**。|
|Jet OLEDB： 全局大容量事务 (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|指示 SQL 大容量事务进行事务处理。|
|Jet OLEDB： 全局部分批量 Ops (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|指示用于打开数据库的密码。|
|Jet OLEDB： 隐式提交同步 (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|指示是否在同步或异步模式下写入内部隐式事务中所做的更改。|
|Jet OLEDB:Lock 延迟 (DBPROP_JETOLEDB_LOCKDELAY)|指示在尝试获取锁后的以前的尝试已失败之前等待毫秒的数。|
|Jet OLEDB:Lock 重试 (DBPROP_JETOLEDB_LOCKRETRY)|指示重复尝试访问锁定的页的次数。|
|Jet OLEDB:Max 缓冲区大小 (DBPROP_JETOLEDB_MAXBUFFERSIZE)|指示最大数量的内存，在千字节为单位，Jet 可以使用开始将更改刷新到磁盘之前。|
|每个文件 (DBPROP_JETOLEDB_MAXLOCKSPERFILE) 的 jet OLEDB:Max 锁|指示 Jet 可以将放置在数据库的锁的最大数目。 默认值为 9500。|
|Jet OLEDB： 新的数据库密码 (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|指示要将设置为此数据库的新密码。 旧密码存储在**Jet OLEDB:Database 密码**。|
|Jet OLEDB:ODBC 命令超时 (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|指示从 Jet 远程 ODBC 查询之前的毫秒数将会超时。|
|Jet OLEDB:Page 锁定表锁 (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK)|指示 Jet 尝试将锁定到表级锁升级之前，必须在事务中锁定多少个页面。 如果此值为 0，锁将永远不会提升。|
|Jet OLEDB:Page 超时 (DBPROP_JETOLEDB_PAGETIMEOUT)|指示 Jet 将检查以确定其缓存是否包含数据库文件过期前等待的毫秒数。|
|Jet OLEDB:Recycle 长时间值页 (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|指示是否应该主动地尝试 Jet 来回收 BLOB 页，则释放时。|
|Jet OLEDB:Registry 路径 (DBPROP_JETOLEDB_REGPATH)|指示包含结果值的 Jet 数据库引擎的 Windows 注册表项。|
|Jet OLEDB:Reset ISAM 统计信息 (DBPROP_JETOLEDB_RESETISAMSTATS)|指示是否架构**记录集**DBSCHEMA_JETOLEDB_ISAMSTATS 应返回性能信息之后重置其性能计数器。|
|Jet OLEDB： 共享异步延迟 (DBPROP_JETOLEDB_SHAREDASYNCDELAY)|指示所最长的时间，以毫秒为单位，Jet 可以延迟异步写入到磁盘时在多用户模式下打开该数据库。|
|Jet oledb： 系统数据库 (DBPROP_JETOLEDB_SYSDBPATH)|指示工作组信息文件 （系统数据库） 的路径和文件名称。|
|Jet OLEDB:Transaction 提交模式 (DBPROP_JETOLEDB_TXNCOMMITMODE)|指示是否 Jet 将数据写入磁盘以同步方式或异步提交事务时。|
|Jet OLEDB:User 提交同步 (DBPROP_JETOLEDB_USERCOMMITSYNC)|指示是否在同步或异步模式下写入事务中所做的更改。|

## <a name="provider-specific-recordset-and-command-properties"></a>提供程序特定的记录集和命令属性
 Jet 提供程序还支持多个提供程序特定**记录集**和**命令**属性。 访问并通过设置这些属性**属性**集合**记录集**或**命令**对象。 表列出 ADO 属性名称和其对应的 OLE DB 属性名，在括号中。

|属性名称|Description|
|-------------------|-----------------|
|Jet OLEDB:Bulk 事务 (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|指示 SQL 大容量操作进行事务处理。 处理时，由于资源延迟，大容量操作可能会失败。|
|Jet OLEDB:Enable Fat 游标 (DBPROP_JETOLEDB_ENABLEFATCURSOR)|指示填充远程行源的记录集时，Jet 是否应缓存多个行。|
|Jet OLEDB:Fat 光标缓存大小 (DBPROP_JETOLEDB_FATCURSORMAXROWS)|使用远程数据存储行缓存时，该值指示缓存的行数。 将忽略此值，除非**Jet OLEDB:Enable Fat 游标**为 True。|
|Jet OLEDB： 不一致 (DBPROP_JETOLEDB_INCONSISTENT)|指示查询结果是否允许不一致的更新。|
|Jet OLEDB： 锁定粒度 (DBPROP_JETOLEDB_LOCKGRANULARITY)|指示是否使用行级锁定打开表。|
|Jet OLEDB:ODBC 传递语句 (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|指示 Jet 应传递中的 SQL 文本**命令**到后端不变的对象。|
|Jet OLEDB:Partial 大容量 Ops (DBPROP_JETOLEDB_BULKPARTIAL)|SQL DML 操作失败时，该值指示 Jet 的行为。|
|通过查询大容量操作 (DBPROP_JETOLEDB_PASSTHROUGHBULKOP) 的 jet OLEDB:Pass|指示是否查询，不返回**记录集**到数据源传递不变。|
|通过查询的 jet OLEDB:Pass 连接字符串 (DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING)|指示使用的 Jet 连接字符串以连接到远程数据存储。 将忽略此值，除非**Jet OLEDB:ODBC 传递语句**为 True。|
|Jet OLEDB： 存储查询 (DBPROP_JETOLEDB_STOREDQUERY)|指示是否应将命令文本解释为存储查询而不是 SQL 命令。|
|Jet OLEDB： 验证在组 (DBPROP_JETOLEDB_VALIDATEONSET) 上的规则|指示当列数据被设置，或提交到数据库所做的更改时是否评估 Jet 验证规则。|

 默认情况下，Microsoft Jet 的 OLE DB 访问接口在读/写模式下打开 Microsoft Jet 数据库。 若要在只读模式下打开一个数据库，设置[模式](../../../ado/reference/ado-api/mode-property-ado.md)属性 ADO**连接**对象传递给**adModeRead**。

## <a name="command-object-usage"></a>命令对象用法
 命令中的文本[命令](../../../ado/reference/ado-api/command-object-ado.md)对象使用的 Microsoft Jet SQL 方言。 可以在命令文本; 中指定返回行的查询、 操作查询，以及表名称但是，存储的过程不支持，并且不应指定。

## <a name="recordset-behavior"></a>记录集行为
 Microsoft Jet 数据库引擎不支持动态游标。 因此，Microsoft Jet 的 OLE DB 访问接口不支持**adLockDynamic**游标类型。 提供程序请求动态游标时，将返回键集游标和重置[游标类型](../../../ado/reference/ado-api/cursortype-property-ado.md)属性以指示的一种[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)返回。 此外，如果可更新**记录集**请求 (**LockType**是**adLockOptimistic**， **adLockBatchOptimistic**，或**adLockPessimistic**) 的提供程序还将返回键集游标和重置**游标类型**属性。

## <a name="dynamic-properties"></a>动态属性
 用于 Microsoft Jet OLE DB 提供程序插入到多个动态属性**属性**集合的未打开[连接](../../../ado/reference/ado-api/connection-object-ado.md)，[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，和[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。

 下表是每个动态属性的 ADO 和 OLE DB 名称交叉。 OLE DB 程序员参考指 ADO 属性名称，术语"Description"。 OLE DB 程序员参考中，你可以找到有关这些属性的详细信息。

## <a name="connection-dynamic-properties"></a>连接的动态属性
 以下属性添加到**属性**集合**连接**对象。

|ADO 属性名称|OLE DB 属性名称|
|-----------------------|--------------------------|
|活动会话|DBPROP_ACTIVESESSIONS|
|异步终止|DBPROP_ASYNCTXNABORT|
|可异步提交|DBPROP_ASYNCTNXCOMMIT|
|自动提交隔离级别|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|目录位置|DBPROP_CATALOGLOCATION|
|目录术语|DBPROP_CATALOGTERM|
|列定义|DBPROP_COLUMNDEFINITION|
|当前目录|DBPROP_CURRENTCATALOG|
|数据源|DBPROP_INIT_DATASOURCE|
|数据源名称|DBPROP_DATASOURCENAME|
|线程处理模型的数据源对象|DBPROP_DSOTHREADMODEL|
|DBMS 名称|DBPROP_DBMSNAME|
|DBMS 版本|DBPROP_DBMSVER|
|按支持进行分组|DBPROP_GROUPBY|
|异类表支持|DBPROP_HETEROGENEOUSTABLES|
|标识符区分大小写|DBPROP_IDENTIFIERCASE|
|隔离级别|DBPROP_SUPPORTEDTXNISOLEVELS|
|隔离保留|DBPROP_SUPPORTEDTXNISORETAIN|
|区域设置标识符|DBPROP_INIT_LCID|
|最大索引大小|DBPROP_MAXINDEXSIZE|
|最大行大小|DBPROP_MAXROWSIZE|
|最大行大小包括 BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|在选择的最大表|DBPROP_MAXTABLESINSELECT|
|“模式”|DBPROP_INIT_MODE|
|多个参数集|DBPROP_MULTIPLEPARAMSETS|
|多个结果|DBPROP_MULTIPLERESULTS|
|多个存储对象|DBPROP_MULTIPLESTORAGEOBJECTS|
|多表更新|DBPROP_MULTITABLEUPDATE|
|NULL 的排序规则顺序|DBPROP_NULLCOLLATION|
|NULL 串联行为|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 版本|DBPROP_PROVIDEROLEDBVER|
|OLE 对象支持|DBPROP_OLEOBJECTS|
|打开行集支持|DBPROP_OPENROWSETSUPPORT|
|通过选择列表中的列进行排序|DBPROP_ORDERBYCOLUMNSINSELECT|
|输出参数可用性|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|通过 Ref 访问器|DBPROP_BYREFACCESSORS|
|Password|DBPROP_AUTH_PASSWORD|
|持久性 ID 类型|DBPROP_PERSISTENTIDTYPE|
|准备中止行为|DBPROP_PREPAREABORTBEHAVIOR|
|准备提交行为|DBPROP_PREPARECOMMITBEHAVIOR|
|过程术语|DBPROP_PROCEDURETERM|
|提示|DBPROP_INIT_PROMPT|
|提供程序的友好名称|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|提供程序版本|DBPROP_PROVIDERVER|
|仅限读取的数据源|DBPROP_DATASOURCEREADONLY|
|在命令行集转换|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|架构术语|DBPROP_SCHEMATERM|
|架构使用情况|DBPROP_SCHEMAUSAGE|
|SQL 支持|DBPROP_SQLSUPPORT|
|结构化的存储|DBPROP_STRUCTUREDSTORAGE|
|子查询支持|DBPROP_SUBQUERIES|
|表术语|DBPROP_TABLETERM|
|事务 DDL|DBPROP_SUPPORTEDTXNDDL|
|用户 ID|DBPROP_AUTH_USERID|
|用户名|DBPROP_USERNAME|
|窗口句柄|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>记录集动态属性
 以下属性添加到**属性**集合**记录集**对象。

|ADO 属性名称|OLE DB 属性名称|
|-----------------------|--------------------------|
|访问顺序|DBPROP_ACCESSORDER|
|仅限追加的行集|DBPROP_APPENDONLY|
|阻止存储对象|DBPROP_BLOCKINGSTORAGEOBJECTS|
|书签类型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|排序的书签|DBPROP_ORDEREDBOOKMARKS|
|缓存延迟的列|DBPROP_CACHEDEFERRED|
|更改插入的行|DBPROP_CHANGEINSERTEDROWS|
|列权限|DBPROP_COLUMNRESTRICT|
|列集通知|DBPROP_NOTIFYCOLUMNSET|
|可写的列|DBPROP_MAYWRITECOLUMN|
|延迟列|DBPROP_DEFERRED|
|延迟存储对象更新|DBPROP_DELAYSTORAGEOBJECTS|
|向后获取|DBPROP_CANFETCHBACKWARDS|
|保存行|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|固定的行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IrowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IrowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IrowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|文本书签|DBPROP_LITERALBOOKMARKS|
|文本行标识|DBPROP_LITERALIDENTITY|
|打开的最大行数|DBPROP_MAXOPENROWS|
|最大挂起行|DBPROP_MAXPENDINGROWS|
|最大行数|DBPROP_MAXROWS|
|内存使用量|DBPROP_MEMORYUSAGE|
|通知粒度|DBPROP_NOTIFICATIONGRANULARITY|
|通知阶段|DBPROP_NOTIFICATIONPHASES|
|事务处理的对象|DBPROP_TRANSACTEDOBJECT|
|可见的其他用户的更改|DBPROP_OTHERUPDATEDELETE|
|其他可见插入|DBPROP_OTHERINSERT|
|拥有更改可见|DBPROP_OWNUPDATEDELETE|
|自己插入可见|DBPROP_OWNINSERT|
|中止时保留|DBPROP_ABORTPRESERVE|
|提交时保留|DBPROP_COMMITPRESERVE|
|快速重新启动|DBPROP_QUICKRESTART|
|可重入事件|DBPROP_REENTRANTEVENTS|
|删除已删除的行|DBPROP_REMOVEDELETED|
|报告多个更改|DBPROP_REPORTMULTIPLECHANGES|
|返回挂起的插入|DBPROP_RETURNPENDINGINSERTS|
|行删除通知|DBPROP_NOTIFYROWDELETE|
|行的第一个更改通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|行插入通知|DBPROP_NOTIFYROWINSERT|
|行的权限|DBPROP_ROWRESTRICT|
|行重新同步通知|DBPROP_NOTIFYROWRESYNCH|
|线程处理模型的行|DBPROP_ROWTHREADMODEL|
|行撤消更改通知|DBPROP_NOTIFYROWUNDOCHANGE|
|行撤消删除通知|DBPROP_NOTIFYROWUNDODELETE|
|行撤消插入通知|DBPROP_NOTIFYROWUNDOINSERT|
|行更新通知|DBPROP_NOTIFYROWUPDATE|
|行集提取位置更改通知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|行集版本通知|DBPROP_NOTIFYROWSETRELEASE|
|向后滚动|DBPROP_CANSCROLLBACKWARDS|
|跳过删除书签|DBPROP_BOOKMARKSKIPPED|
|强行标识|DBPROP_STRONGITDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用书签|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令动态属性
 以下属性添加到**属性**集合**命令**对象。

|ADO 属性名称|OLE DB 属性名称|
|-----------------------|--------------------------|
|访问顺序|DBPROP_ACCESSORDER|
|仅限追加的行集|DBPROP_APPENDONLY|
|阻止存储对象|DBPROP_BLOCKINGSTORAGEOBJECTS|
|书签类型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|更改插入的行|DBPROP_CHANGEINSERTEDROWS|
|列权限|DBPROP_COLUMNRESTRICT|
|列集通知|DBPROP_NOTIFYCOLUMNSET|
|延迟列|DBPROP_DEFERRED|
|延迟存储对象更新|DBPROP_DELAYSTORAGEOBJECTS|
|向后获取|DBPROP_CANFETCHBACKWARDS|
|保存行|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|固定的行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IrowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IrowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IrowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|文本书签|DBPROP_LITERALBOOKMARKS|
|文本行标识|DBPROP_LITERALIDENTITY|
|锁定模式|DBPROP_LOCKMODE|
|打开的最大行数|DBPROP_MAXOPENROWS|
|最大挂起行|DBPROP_MAXPENDINGROWS|
|最大行数|DBPROP_MAXROWS|
|通知粒度|DBPROP_NOTIFICATIONGRANULARITY|
|通知阶段|DBPROP_NOTIFICATIONPHASES|
|事务处理的对象|DBPROP_TRANSACTEDOBJECT|
|可见的其他用户的更改|DBPROP_OTHERUPDATEDELETE|
|其他可见插入|DBPROP_OTHERINSERT|
|拥有更改可见|DBPROP_OWNUPDATEDELETE|
|自己插入可见|DBPROP_OWNINSERT|
|中止时保留|DBPROP_ABORTPRESERVE|
|提交时保留|DBPROP_COMMITPRESERVE|
|快速重新启动|DBPROP_QUICKRESTART|
|可重入事件|DBPROP_REENTRANTEVENTS|
|删除已删除的行|DBPROP_REMOVEDELETED|
|报告多个更改|DBPROP_REPORTMULTIPLECHANGES|
|返回挂起的插入|DBPROP_RETURNPENDINGINSERTS|
|行删除通知|DBPROP_NOTIFYROWDELETE|
|行的第一个更改通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|行插入通知|DBPROP_NOTIFYROWINSERT|
|行的权限|DBPROP_ROWRESTRICT|
|行重新同步通知|DBPROP_NOTIFYROWRESYNCH|
|线程处理模型的行|DBPROP_ROWTHREADMODEL|
|行撤消更改通知|DBPROP_NOTIFYROWUNDOCHANGE|
|行撤消删除通知|DBPROP_NOTIFYROWUNDODELETE|
|行撤消插入通知|DBPROP_NOTIFYROWUNDOINSERT|
|行更新通知|DBPROP_NOTIFYROWUPDATE|
|行集提取位置更改通知|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|行集版本通知|DBPROP_NOTIFYROWSETRELEASE|
|向后滚动|DBPROP_CANSCROLLBACKWARDS|
|在插入服务器数据|DBPROP_SERVERDATAONINSERT|
|跳过删除书签|DBPROP_BOOKMARKSKIP|
|强行标识|DBPROP_STRONGIDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用书签|DBPROP_BOOKMARKS|

 特定的实现详细信息和有关 for Microsoft Jet OLE DB 访问接口的功能信息，请参阅[Jet 提供程序](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx)OLE DB 文档中。
