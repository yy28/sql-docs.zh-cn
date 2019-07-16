---
title: 适用于 Microsoft Jet 的 Microsoft OLE DB 提供程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69d88aebe25f6cfa5490cce736c05780b87eee6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926646"
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Microsoft OLE DB Provider for Microsoft Jet 概述
适用于 Microsoft Jet OLE DB 访问接口允许访问 Microsoft Jet 数据库的 ADO。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到此提供程序，请设置*提供程序*的参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性设置为以下：

```vb
Microsoft.Jet.OLEDB.4.0
```

 读取[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性也将返回此字符串。

## <a name="typical-connection-string"></a>典型的连接字符串
 此提供程序的典型的连接字符串是：

```vb
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 该字符串包含这些关键字：

|关键字|描述|
|-------------|-----------------|
|**提供程序**|指定 Microsoft Jet 的 OLE DB 访问接口。|
|**数据源**|指定数据库路径和文件名 (例如， `c:\Northwind.mdb`)。|
|**用户 ID**|指定用户名称。 如果未指定此关键字，在字符串中，"`admin`"，默认情况下使用。|
|**密码**|指定用户密码。 如果未指定此关键字，则为空字符串 ("")，默认情况下使用。|

> [!NOTE]
>  如果您要连接到的数据源提供程序支持 Windows 身份验证，则应指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是用户 ID 和密码在连接字符串中的信息。

## <a name="provider-specific-connection-parameters"></a>提供程序特定的连接参数
 适用于 Microsoft Jet OLE DB 访问接口支持除由 ADO 定义多个特定于提供程序的动态属性。 与所有其他一样**连接**参数，它们可以使用设置**属性**的集合**连接**对象或作为连接字符串的一部分。

 下表列出了这些属性以及相应的 OLE DB 属性名称在括号中。

|参数|描述|
|---------------|-----------------|
|Jet OLEDB:Compact 回收的空间量 (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|指示以字节为单位，可以通过压缩数据库来回收的空间量的估计值。 建立数据库连接之后，此值才有效。|
|Jet OLEDB:Connection 控件 (DBPROP_JETOLEDB_CONNECTIONCONTROL)|指示用户是否可以连接到数据库。|
|Jet OLEDB： 创建系统数据库 (DBPROP_JETOLEDB_CREATESYSTEMDATABASE)|指示是否应创建新的数据源时创建系统数据库。|
|Jet oledb： 数据库锁定模式 (DBPROP_JETOLEDB_DATABASELOCKMODE)|指示此数据库的锁定模式。 若要打开的数据库的第一个用户确定数据库处于打开状态时所用的模式。|
|Jet oledb： 数据库密码 (DBPROP_JETOLEDB_DATABASEPASSWORD)|指示数据库密码。|
|Jet OLEDB： 不要复制 Compact (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE) 上的区域设置|指示是否压缩数据库时，Jet 应复制的区域设置信息。|
|Jet OLEDB： 加密数据库 (DBPROP_JETOLEDB_ENCRYPTDATABASE)|指示是否应加密压缩的数据库。 如果未设置此属性，也加密原始数据库将加密压缩的数据库。|
|Jet OLEDB:Engine 类型 (DBPROP_JETOLEDB_ENGINE)|指示用于访问当前数据存储区的存储引擎。|
|Jet OLEDB:Exclusive 异步延迟 (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|指示时间，以毫秒为单位，Jet 可以延迟异步写入到磁盘时以独占方式打开该数据库的最大的长度。<br /><br /> 将忽略此属性，除非**Jet OLEDB:Flush 事务超时**设置为 0。|
|Jet OLEDB:Flush 事务超时值 (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|指示的时间等待的异步写入缓存中存储的数据实际写入到磁盘。 此设置替代的值**Jet OLEDB： 共享异步延迟**并**Jet OLEDB:Exclusive 异步延迟**。|
|Jet OLEDB： 全局大容量事务 (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|指示 SQL 大容量事务进行事务处理。|
|Jet OLEDB： 全局部分大容量操作 (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|指示用于打开数据库的密码。|
|Jet OLEDB： 隐式提交同步 (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|指示是否将在内部隐式事务中所做的更改写入同步或异步模式中。|
|Jet OLEDB:Lock 延迟 (DBPROP_JETOLEDB_LOCKDELAY)|指示要尝试获取锁后先前的尝试已失败之前等待毫秒的数。|
|Jet OLEDB:Lock 重试 (DBPROP_JETOLEDB_LOCKRETRY)|指示重复尝试访问已锁定的页的次数。|
|Jet OLEDB:Max 缓冲区大小 (DBPROP_JETOLEDB_MAXBUFFERSIZE)|指示最大数量的内存，在千字节为单位，Jet 可以使用前更改刷新到磁盘。|
|每个文件 (DBPROP_JETOLEDB_MAXLOCKSPERFILE) jet OLEDB:Max 锁|指示 Jet 可以将放置在数据库的锁的最大数目。 默认值为 9500。|
|Jet OLEDB： 新的数据库密码 (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|指示要为此数据库设置的新密码。 旧密码存储在**Jet oledb： 数据库密码**。|
|Jet OLEDB:ODBC 命令超时 (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|指示远程 ODBC 查询从 Jet 之前的毫秒数将会超时。|
|Jet OLEDB:Page 锁定到表锁 (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK)|指示 Jet 尝试升级到表锁的锁之前，必须在事务中锁定多少页。 如果此值为 0，永远不会提升该锁。|
|Jet OLEDB:Page 超时 (DBPROP_JETOLEDB_PAGETIMEOUT)|指示 Jet 检查其缓存已与数据库文件的过期之前要等待的毫秒数。|
|Jet OLEDB:Recycle 长时间值页 (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|指示是否 Jet 应积极地尝试回收 BLOB 页面时也将释放。|
|Jet OLEDB:Registry 路径 (DBPROP_JETOLEDB_REGPATH)|指示包含值的 Jet 数据库引擎的 Windows 注册表项。|
|Jet OLEDB:Reset ISAM 统计信息 (DBPROP_JETOLEDB_RESETISAMSTATS)|指示是否在架构**记录集**DBSCHEMA_JETOLEDB_ISAMSTATS 应在返回的性能信息后重置其性能计数器。|
|Jet OLEDB： 共享异步延迟 (DBPROP_JETOLEDB_SHAREDASYNCDELAY)|指示的最长的时间，以毫秒为单位，Jet 可以延迟异步写入到磁盘时在多用户模式下打开该数据库。|
|Jet oledb： 系统数据库 (DBPROP_JETOLEDB_SYSDBPATH)|指示工作组信息文件 （系统数据库） 路径和文件名。|
|Jet OLEDB:Transaction 提交模式 (DBPROP_JETOLEDB_TXNCOMMITMODE)|指示是否 Jet 将数据写入磁盘以同步方式还是以异步方式提交事务时。|
|Jet OLEDB:User 提交同步 (DBPROP_JETOLEDB_USERCOMMITSYNC)|指示是否将在事务中所做的更改写入同步或异步模式中。|

## <a name="provider-specific-recordset-and-command-properties"></a>特定于提供程序的记录集和命令属性
 Jet 访问接口还支持多个提供程序特定**记录集**并**命令**属性。 这些属性是访问，通过设置**属性**系列**记录集**或**命令**对象。 表列出了 ADO 的属性名称和其相应的 OLE DB 属性名称在括号中。

|属性名|描述|
|-------------------|-----------------|
|Jet OLEDB:Bulk 事务 (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|指示 SQL 大容量操作进行事务处理。 事务处理，由于资源延迟时，大容量操作可能会失败。|
|Jet OLEDB:Enable Fat 游标 (DBPROP_JETOLEDB_ENABLEFATCURSOR)|指示是否填充远程行源的记录集时，Jet 应缓存多个行。|
|Jet OLEDB:Fat 游标缓存大小 (DBPROP_JETOLEDB_FATCURSORMAXROWS)|使用远程数据存储行缓存时，该值指示缓存的行数。 将忽略此值，除非**Jet OLEDB:Enable Fat 游标**为 True。|
|Jet OLEDB： 不一致 (DBPROP_JETOLEDB_INCONSISTENT)|指示查询结果是否允许不一致的更新。|
|Jet OLEDB： 锁定粒度 (DBPROP_JETOLEDB_LOCKGRANULARITY)|指示是否使用行级锁定打开表。|
|Jet OLEDB:ODBC 传递语句 (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|指示 Jet 应传递中的 SQL 文本**命令**到后端不变的对象。|
|Jet OLEDB:Partial 大容量操作 (DBPROP_JETOLEDB_BULKPARTIAL)|SQL DML 操作失败时指示 Jet 的行为。|
|通过查询大容量操作 (DBPROP_JETOLEDB_PASSTHROUGHBULKOP) jet OLEDB:Pass|指示是否查询，则不返回**记录集**到数据源传递未更改。|
|通过查询 jet OLEDB:Pass 连接字符串 (DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING)|指示使用的 Jet 连接字符串连接到远程数据存储。 将忽略此值，除非**Jet OLEDB:ODBC 直通语句**为 True。|
|Jet OLEDB： 存储查询 (DBPROP_JETOLEDB_STOREDQUERY)|指示是否应将命令文本解释为存储查询而不是 SQL 命令。|
|Jet OLEDB： 验证规则集 (DBPROP_JETOLEDB_VALIDATEONSET)|指示当列数据集或提交到数据库所做的更改时是否计算 Jet 验证规则。|

 默认情况下，适用于 Microsoft Jet OLE DB 访问接口以读/写模式打开 Microsoft Jet 数据库。 若要在只读模式下打开数据库，请设置[模式下](../../../ado/reference/ado-api/mode-property-ado.md)属性上 ADO**连接**对象传递给**adModeRead**。

## <a name="command-object-usage"></a>命令对象使用
 命令中的文本[命令](../../../ado/reference/ado-api/command-object-ado.md)对象使用的 Microsoft Jet SQL 方言。 可以在命令文本; 中指定返回行的查询、 操作查询和表名称但是，存储的过程不受支持，并且不应指定。

## <a name="recordset-behavior"></a>记录集行为
 Microsoft Jet 数据库引擎不支持动态游标。 因此，适用于 Microsoft Jet OLE DB 访问接口不支持**adLockDynamic**游标类型。 提供程序动态游标请求时，将返回由键集游标和重置[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)属性来指示类型的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)返回。 此外，如果可更新**记录集**请求 (**LockType**是**adLockOptimistic**， **adLockBatchOptimistic**，或**adLockPessimistic**) 的提供程序还将返回由键集游标和重置**CursorType**属性。

## <a name="dynamic-properties"></a>动态属性
 适用于 Microsoft Jet OLE DB 访问接口将插入到多个动态属性**属性**的未打开集合[连接](../../../ado/reference/ado-api/connection-object-ado.md)，[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，以及[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。

 下表是 ADO 和 OLE DB 名称的每个动态属性的交叉索引。 OLE DB 程序员参考指 ADO 属性名称，术语"Description"。 在 OLE DB 程序员参考中，可以找到有关这些属性的详细信息。

## <a name="connection-dynamic-properties"></a>连接的动态属性
 下列属性被添加到**属性**集合的**连接**对象。

|ADO 属性名称|OLE DB 属性名|
|-----------------------|--------------------------|
|活动会话|DBPROP_ACTIVESESSIONS|
|异步终止|DBPROP_ASYNCTXNABORT|
|可异步提交|DBPROP_ASYNCTNXCOMMIT|
|自动提交隔离级别|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|目录位置|DBPROP_CATALOGLOCATION|
|目录项|DBPROP_CATALOGTERM|
|列定义|DBPROP_COLUMNDEFINITION|
|当前目录|DBPROP_CURRENTCATALOG|
|数据源|DBPROP_INIT_DATASOURCE|
|数据源名称|DBPROP_DATASOURCENAME|
|数据源对象线程模型|DBPROP_DSOTHREADMODEL|
|DBMS 名称|DBPROP_DBMSNAME|
|DBMS 版本|DBPROP_DBMSVER|
|支持按分组|DBPROP_GROUPBY|
|异类表支持|DBPROP_HETEROGENEOUSTABLES|
|标识符区分大小写|DBPROP_IDENTIFIERCASE|
|隔离级别|DBPROP_SUPPORTEDTXNISOLEVELS|
|隔离保持|DBPROP_SUPPORTEDTXNISORETAIN|
|区域设置标识符|DBPROP_INIT_LCID|
|最大索引大小|DBPROP_MAXINDEXSIZE|
|最大行大小|DBPROP_MAXROWSIZE|
|最大行大小包括 BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|最大的表中选择|DBPROP_MAXTABLESINSELECT|
|模式|DBPROP_INIT_MODE|
|多个参数集|DBPROP_MULTIPLEPARAMSETS|
|多个结果|DBPROP_MULTIPLERESULTS|
|多个存储对象|DBPROP_MULTIPLESTORAGEOBJECTS|
|多表更新|DBPROP_MULTITABLEUPDATE|
|空排序|DBPROP_NULLCOLLATION|
|空串联行为|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 版本|DBPROP_PROVIDEROLEDBVER|
|OLE 对象支持|DBPROP_OLEOBJECTS|
|打开行集合支持|DBPROP_OPENROWSETSUPPORT|
|按选择列表中的列进行排序|DBPROP_ORDERBYCOLUMNSINSELECT|
|输出参数可用性|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|传递 By Ref 访问器|DBPROP_BYREFACCESSORS|
|Password|DBPROP_AUTH_PASSWORD|
|持久性 ID 类型|DBPROP_PERSISTENTIDTYPE|
|准备中止行为|DBPROP_PREPAREABORTBEHAVIOR|
|准备提交行为|DBPROP_PREPARECOMMITBEHAVIOR|
|过程项|DBPROP_PROCEDURETERM|
|提示|DBPROP_INIT_PROMPT|
|提供程序友好名称|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|提供程序版本|DBPROP_PROVIDERVER|
|只读数据源|DBPROP_DATASOURCEREADONLY|
|在命令行集转换|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|架构项|DBPROP_SCHEMATERM|
|架构使用情况|DBPROP_SCHEMAUSAGE|
|SQL 支持|DBPROP_SQLSUPPORT|
|结构化的存储|DBPROP_STRUCTUREDSTORAGE|
|子查询支持|DBPROP_SUBQUERIES|
|表项|DBPROP_TABLETERM|
|事务 DDL|DBPROP_SUPPORTEDTXNDDL|
|用户 ID|DBPROP_AUTH_USERID|
|用户名|DBPROP_USERNAME|
|窗口句柄|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>记录集动态属性
 以下属性添加到**属性**系列**记录集**对象。

|ADO 属性名称|OLE DB 属性名|
|-----------------------|--------------------------|
|访问顺序|DBPROP_ACCESSORDER|
|仅限追加的行集|DBPROP_APPENDONLY|
|模块化存储对象|DBPROP_BLOCKINGSTORAGEOBJECTS|
|书签类型|DBPROP_BOOKMARKTYPE|
|可存为书签|DBPROP_IROWSETLOCATE|
|书签已排序|DBPROP_ORDEREDBOOKMARKS|
|缓存延迟的列|DBPROP_CACHEDEFERRED|
|更改插入的行|DBPROP_CHANGEINSERTEDROWS|
|列权限|DBPROP_COLUMNRESTRICT|
|列设置通知|DBPROP_NOTIFYCOLUMNSET|
|可写的列|DBPROP_MAYWRITECOLUMN|
|延迟列|DBPROP_DEFERRED|
|延迟存储对象更新|DBPROP_DELAYSTORAGEOBJECTS|
|向后提取|DBPROP_CANFETCHBACKWARDS|
|保留行|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|固定行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IrowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|书签|DBPROP_LITERALBOOKMARKS|
|行标识|DBPROP_LITERALIDENTITY|
|最大打开行数|DBPROP_MAXOPENROWS|
|最大挂起行数|DBPROP_MAXPENDINGROWS|
|最大行数|DBPROP_MAXROWS|
|内存使用量|DBPROP_MEMORYUSAGE|
|通知间隔|DBPROP_NOTIFICATIONGRANULARITY|
|通知阶段|DBPROP_NOTIFICATIONPHASES|
|事务处理的对象|DBPROP_TRANSACTEDOBJECT|
|其他可见更改|DBPROP_OTHERUPDATEDELETE|
|其他可见插入|DBPROP_OTHERINSERT|
|自己的可见更改|DBPROP_OWNUPDATEDELETE|
|自己的可见插入|DBPROP_OWNINSERT|
|中止时保留|DBPROP_ABORTPRESERVE|
|提交时保留|DBPROP_COMMITPRESERVE|
|快速重新启动|DBPROP_QUICKRESTART|
|可重入事件|DBPROP_REENTRANTEVENTS|
|删除已删除的行|DBPROP_REMOVEDELETED|
|报告多个更改|DBPROP_REPORTMULTIPLECHANGES|
|返回挂起的插入|DBPROP_RETURNPENDINGINSERTS|
|行删除通知|DBPROP_NOTIFYROWDELETE|
|行首次更改通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|行插入通知|DBPROP_NOTIFYROWINSERT|
|行特权|DBPROP_ROWRESTRICT|
|行重同步通知|DBPROP_NOTIFYROWRESYNCH|
|行线程模型|DBPROP_ROWTHREADMODEL|
|行撤消更改通知|DBPROP_NOTIFYROWUNDOCHANGE|
|行撤消删除通知|DBPROP_NOTIFYROWUNDODELETE|
|行撤消插入通知|DBPROP_NOTIFYROWUNDOINSERT|
|行更新通知|DBPROP_NOTIFYROWUPDATE|
|行集提取位置更改通知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|行集合释放通知|DBPROP_NOTIFYROWSETRELEASE|
|向后滚动|DBPROP_CANSCROLLBACKWARDS|
|跳过删除的书签|DBPROP_BOOKMARKSKIPPED|
|强行标识|DBPROP_STRONGITDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用书签|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令动态属性
 以下属性添加到**属性**系列**命令**对象。

|ADO 属性名称|OLE DB 属性名|
|-----------------------|--------------------------|
|访问顺序|DBPROP_ACCESSORDER|
|仅限追加的行集|DBPROP_APPENDONLY|
|模块化存储对象|DBPROP_BLOCKINGSTORAGEOBJECTS|
|书签类型|DBPROP_BOOKMARKTYPE|
|可存为书签|DBPROP_IROWSETLOCATE|
|更改插入的行|DBPROP_CHANGEINSERTEDROWS|
|列权限|DBPROP_COLUMNRESTRICT|
|列设置通知|DBPROP_NOTIFYCOLUMNSET|
|延迟列|DBPROP_DEFERRED|
|延迟存储对象更新|DBPROP_DELAYSTORAGEOBJECTS|
|向后提取|DBPROP_CANFETCHBACKWARDS|
|保留行|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|固定行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IrowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|书签|DBPROP_LITERALBOOKMARKS|
|行标识|DBPROP_LITERALIDENTITY|
|锁模式|DBPROP_LOCKMODE|
|最大打开行数|DBPROP_MAXOPENROWS|
|最大挂起行数|DBPROP_MAXPENDINGROWS|
|最大行数|DBPROP_MAXROWS|
|通知间隔|DBPROP_NOTIFICATIONGRANULARITY|
|通知阶段|DBPROP_NOTIFICATIONPHASES|
|事务处理的对象|DBPROP_TRANSACTEDOBJECT|
|其他可见更改|DBPROP_OTHERUPDATEDELETE|
|其他可见插入|DBPROP_OTHERINSERT|
|自己的可见更改|DBPROP_OWNUPDATEDELETE|
|自己的可见插入|DBPROP_OWNINSERT|
|中止时保留|DBPROP_ABORTPRESERVE|
|提交时保留|DBPROP_COMMITPRESERVE|
|快速重新启动|DBPROP_QUICKRESTART|
|可重入事件|DBPROP_REENTRANTEVENTS|
|删除已删除的行|DBPROP_REMOVEDELETED|
|报告多个更改|DBPROP_REPORTMULTIPLECHANGES|
|返回挂起的插入|DBPROP_RETURNPENDINGINSERTS|
|行删除通知|DBPROP_NOTIFYROWDELETE|
|行首次更改通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|行插入通知|DBPROP_NOTIFYROWINSERT|
|行特权|DBPROP_ROWRESTRICT|
|行重同步通知|DBPROP_NOTIFYROWRESYNCH|
|行线程模型|DBPROP_ROWTHREADMODEL|
|行撤消更改通知|DBPROP_NOTIFYROWUNDOCHANGE|
|行撤消删除通知|DBPROP_NOTIFYROWUNDODELETE|
|行撤消插入通知|DBPROP_NOTIFYROWUNDOINSERT|
|行更新通知|DBPROP_NOTIFYROWUPDATE|
|行集提取位置更改通知|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|行集合释放通知|DBPROP_NOTIFYROWSETRELEASE|
|向后滚动|DBPROP_CANSCROLLBACKWARDS|
|服务器在插入数据|DBPROP_SERVERDATAONINSERT|
|跳过删除的书签|DBPROP_BOOKMARKSKIP|
|强行标识|DBPROP_STRONGIDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用书签|DBPROP_BOOKMARKS|

 有关特定的实现详细信息和有关适用于 Microsoft Jet OLE DB 访问接口的功能信息，请参阅[Jet 访问接口](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx)OLE DB 文档中。
