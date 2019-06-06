---
title: 对于 SQL Server Microsoft OLE DB 提供程序 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f083f62a67a2255b59fe9ca7cffc03e5aaf5f0a1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701184"
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>有关 SQL Server 概述 Microsoft OLE DB 提供程序
Microsoft OLE DB 提供程序的 SQL Server，SQLOLEDB，允许 ADO 访问 Microsoft SQL Server。

> [!IMPORTANT]
> Microsoft OLE DB Provider for SQL Server (SQLOLEDB) 保持不推荐使用，不建议用于新的开发工作。 相反，使用新[Microsoft OLE DB 驱动程序适用于 SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) 这将使用最新的服务器功能更新。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到此提供程序，将*提供商*参数[连接字符串](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性：

```vb
SQLOLEDB
```

 此值还可以设置或读取使用[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性。

## <a name="typical-connection-string"></a>典型的连接字符串
 此提供程序的典型的连接字符串是：

```vb
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 该字符串包含这些关键字：

|关键字|Description|
|-------------|-----------------|
|**提供程序**|指定 SQL Server 的 OLE DB 提供的程序。|
|**数据源**或**服务器**|指定的服务器的名称。|
|**初始目录**或**数据库**|指定服务器上的数据库的名称。|
|**用户 ID**或**uid**|指定用户名称 （对于 SQL Server 身份验证）。|
|**密码**或**密码**|指定用户密码 （对于 SQL Server 身份验证）。|

> [!NOTE]
>  如果您要连接到的数据源提供程序支持 Windows 身份验证，则应指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是用户 ID 和密码在连接字符串中的信息。

## <a name="provider-specific-connection-parameters"></a>提供程序特定的连接参数
 此提供程序支持除 ADO 定义的多个提供程序特定的连接参数。 如 ADO 连接的属性，使用这些特定于提供程序的属性可以设置通过[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合的[连接](../../../ado/reference/ado-api/connection-object-ado.md)或可被设置为的一部分**连接字符串**.

|参数|Description|
|---------------|-----------------|
|Trusted_Connection|指示用户身份验证模式。 此属性可以设置为**是**或**No**。 默认值是**No**。 如果将此属性设置为**是**，SQLOLEDB 使用 Microsoft Windows NT 身份验证模式来授权用户访问指定的 SQL Server 数据库**位置**和[数据源](../../../ado/reference/ado-api/datasource-property-ado.md)属性的值。 如果将此属性设置为**No**，SQLOLEDB 使用混合模式来授权用户访问 SQL Server 数据库。 在中指定的 SQL Server 登录和密码**用户 Id**和**密码**属性。|
|当前语言|指示 SQL Server 语言名称。 标识用于系统消息选择和格式化的语言。 语言必须安装在 SQL Server 中，否则为连接将失败的开始。|
|网络地址|指示指定的 SQL Server 的网络地址**位置**属性。|
|网络库|指示用于通信与 SQL Server 网络库 (DLL) 的名称。 该名称不应当包含路径或 .dll 文件扩展名。 由 SQL Server 客户端配置提供默认值。|
|使用过程进行准备|确定在准备命令时，SQL Server 是否创建临时存储的过程 (通过**准备**属性)。|
|自动翻译|指示是否将 OEM/ANSI 字符转换。 可以将此属性设置为**为**或**False**。 默认值是 **True**秒。 如果将此属性设置为**为**，SQLOLEDB 执行 OEM/ANSI 字符转换时，从中检索或发送到 SQL Server 的多字节字符字符串。 如果将此属性设置为**False**，SQLOLEDB 的多字节字符字符串数据不执行 OEM/ANSI 字符转换。|
|Packet Size|指示网络数据包的大小以字节为单位。 数据包大小属性值必须介于 512 和 32767 之间。 默认的 SQLOLEDB 网络包大小为 4096。|
|应用程序名称|指示客户端应用程序的名称。|
|工作站 ID|一个字符串，它标识工作站。|

## <a name="command-object-usage"></a>命令对象使用
 SQLOLEDB 接受综合 ODBC、 ANSI 和特定于 SQL Server 的事务处理 SQL 语法有效。 例如，以下 SQL 语句使用 ODBC SQL 转义序列指定 LCASE 字符串函数：

```sql
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE 返回一个字符串，将所有大写字母字符转换为相应的小写字母字符。 ANSI SQL 字符串函数低执行相同的操作，因此下面的 SQL 语句是 ANSI 等效于前面提到的 ODBC 语句：

```sql
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB 成功地处理语句时指定的命令文本为两种形式。

## <a name="stored-procedures"></a>存储过程
 当执行 SQL Server 存储过程使用 SQLOLEDB 命令时，在命令文本中使用 ODBC 过程调用的转义序列。 SQLOLEDB 然后使用 SQL Server 的远程过程调用机制优化命令处理的时间。 例如，下面的 ODBC SQL 语句是首选的命令文本移动事务处理 SQL 窗体：

## <a name="odbc-sql"></a>ODBC SQL

```vb
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```sql
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>SQL Server 功能
 可以使用 SQL Server 使用 ADO XML**命令**输入和检索结果 XML 流格式，而不是在**记录集**对象。 有关详细信息，请参阅[命令输入使用流](../../../ado/guide/data/command-streams.md)和[到流中检索结果集](../../../ado/guide/data/retrieving-resultsets-into-streams.md)。

### <a name="accessing-sqlvariant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>访问使用 MDAC 2.7、 MDAC 2.8 或 Windows DAC 6.0 sql_variant 数据
 Microsoft SQL Server 具有一个名为的数据类型**sql_variant**。 类似于 OLE DB 的**DBTYPE_VARIANT**，则**sql_variant**数据类型可以存储多种不同类型的数据。 但是，有几个主要区别**DBTYPE_VARIANT**并**sql_variant**。 ADO 还可以处理作为存储的数据**sql_variant**方式不同于它如何处理其他数据类型值。 以下列表介绍了需要考虑访问 SQL Server 数据类型的列中存储时的问题**sql_variant**。

-   在 MDAC 2.7、 MDAC 2.8 和 Windows 数据访问组件 (Windows DAC) 6.0 中，SQL Server 的 OLE DB 访问接口支持**sql_variant**类型。 对于 ODBC OLE DB 提供程序却没有。

-   **Sql_variant**类型不完全匹配**DBTYPE_VARIANT**数据类型。  **Sql_variant**类型支持几个新的子类型不受**DBTYPE_VARIANT**包括**GUID**， **ANSI** (非 UNICODE)字符串，并**BIGINT**。 使用子类型不在前面列出的那些才能正常工作。

-   **Sql_variant**子类型**数值**不符**DBTYPE_DECIMAL**的大小。

-   多个数据类型强制转换将导致类型不匹配。 例如，将强制转换**sql_variant**使用的子类型**GUID**到**DBTYPE_VARIANT**会导致的子类型**safearray**（字节）. 将此类型转换回**sql_variant**将导致新的子类型**数组**（字节）。

-   **记录集**包含的字段**sql_variant**数据可远程处理 （封送处理） 或持久化的才**sql_variant**包含特定的子类型。 尝试远程或将数据保存以下不受支持的子类型将导致运行时错误 （不受支持的转换） 从 Microsoft 持久性提供程序 (MSPersist):**VT_VARIANT**， **VT_RECORD**， **VT_ILLEGAL**， **VT_UNKNOWN**， **VT_BSTR**，和**VT_DISPATCH。**

-   MDAC 2.7、 MDAC 2.8 和 Windows DAC 6.0 中的 SQL Server 的 OLE DB 访问接口的一个名为的动态属性**允许本机变体**，其名称所示，允许开发人员访问**sql_variant**中相对于其本机窗体**DBTYPE_VARIANT**。 如果将此属性设置，以及**记录集**时打开客户端游标引擎 (**adUseClient**)、 **Recordset.Open**调用将失败。 如果设置此属性，然后**记录集**使用服务器游标打开 (**adUseServer**)，则**Recordset.Open**调用将成功，但访问类型的列**sql_variant**将产生错误。

-   在客户端应用程序使用 MDAC 2.5 **sql_variant**数据可用于针对 Microsoft SQL Server 的查询。 但是，值**sql_variant**数据被视为字符串。 此类客户端应用程序应该升级到 MDAC 2.7、 MDAC 2.8 或 Windows DAC 6.0。

## <a name="recordset-behavior"></a>记录集行为
 SQLOLEDB 不能使用 SQL Server 游标支持许多命令生成的多结果。 如果使用者请求需要 SQL Server 游标支持一个记录集时，如果所用的命令文本生成多个单个记录集作为其结果，就会出错。

 SQL Server 游标支持可滚动的 SQLOLEDB 记录集。 SQL Server 对施加限制写到数据库的其他用户所做更改的游标。 具体来说，某些游标中的行不能进行排序，并试图创建记录集使用包含 SQL ORDER BY 子句的命令可能会失败。

## <a name="dynamic-properties"></a>动态属性
 Microsoft OLE DB 提供程序的 SQL Server 将插入到多个动态属性**属性**集合未打开[连接](../../../ado/reference/ado-api/connection-object-ado.md)，[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，和[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。

 下表是 ADO 和 OLE DB 名称的每个动态属性的交叉索引。 OLE DB 程序员参考引用 ADO 属性名称术语"说明"。 在 OLE DB 程序员参考中，可以找到有关这些属性的详细信息。 搜索索引中的 OLE DB 属性名称，或参阅[附录 c:OLE DB 属性](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292)。

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
|连接超时值|DBPROP_INIT_TIMEOUT|
|当前目录|DBPROP_CURRENTCATALOG|
|数据源|DBPROP_INIT_DATASOURCE|
|数据源名称|DBPROP_DATASOURCENAME|
|数据源对象线程模型|DBPROP_DSOTHREADMODEL|
|DBMS 名称|DBPROP_DBMSNAME|
|DBMS 版本|DBPROP_DBMSVER|
|扩展属性|DBPROP_INIT_PROVIDERSTRING|
|支持按分组|DBPROP_GROUPBY|
|异类表支持|DBPROP_HETEROGENEOUSTABLES|
|标识符区分大小写|DBPROP_IDENTIFIERCASE|
|初始目录|DBPROP_INIT_CATALOG|
|隔离级别|DBPROP_SUPPORTEDTXNISOLEVELS|
|隔离保持|DBPROP_SUPPORTEDTXNISORETAIN|
|区域设置标识符|DBPROP_INIT_LCID|
|最大索引大小|DBPROP_MAXINDEXSIZE|
|最大行大小|DBPROP_MAXROWSIZE|
|最大行大小包括 BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|最大的表中选择|DBPROP_MAXTABLESINSELECT|
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
|持久性安全信息|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
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
|模块化存储对象|DBPROP_BLOCKINGSTORAGEOBJECTS|
|书签类型|DBPROP_BOOKMARKTYPE|
|可存为书签|DBPROP_IROWSETLOCATE|
|更改插入的行|DBPROP_CHANGEINSERTEDROWS|
|列权限|DBPROP_COLUMNRESTRICT|
|列设置通知|DBPROP_NOTIFYCOLUMNSET|
|命令超时|DBPROP_COMMANDTIMEOUT|
|延迟列|DBPROP_DEFERRED|
|延迟存储对象更新|DBPROP_DELAYSTORAGEOBJECTS|
|向后提取|DBPROP_CANFETCHBACKWARDS|
|保留行|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|固定行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IrowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|书签|DBPROP_LITERALBOOKMARKS|
|行标识|DBPROP_LITERALIDENTITY|
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
|行集提取位置更改通知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|行集合释放通知|DBPROP_NOTIFYROWSETRELEASE|
|向后滚动|DBPROP_CANSCROLLBACKWARDS|
|服务器游标|DBPROP_SERVERCURSOR|
|跳过删除的书签|DBPROP_BOOKMARKSKIPPED|
|强行标识|DBPROP_STRONGITDENTITY|
|唯一行|DBPROP_UNIQUEROWS|
|可更新性|DBPROP_UPDATABILITY|
|使用书签|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令动态属性
 以下属性添加到**属性**系列**命令**对象。

|ADO 属性名称|OLE DB 属性名|
|-----------------------|--------------------------|
|访问顺序|DBPROP_ACCESSORDER|
|基路径|SSPROP_STREAM_BASEPATH|
|模块化存储对象|DBPROP_BLOCKINGSTORAGEOBJECTS|
|书签类型|DBPROP_BOOKMARKTYPE|
|可存为书签|DBPROP_IROWSETLOCATE|
|更改插入的行|DBPROP_CHANGEINSERTEDROWS|
|列权限|DBPROP_COLUMNRESTRICT|
|列设置通知|DBPROP_NOTIFYCOLUMNSET|
|内容类型|SSPROP_STREAM_CONTENTTYPE|
|游标自动提取|SSPROP_CURSORAUTOFETCH|
|延迟列|DBPROP_DEFERRED|
|延迟准备|SSPROP_DEFERPREPARE|
|延迟存储对象更新|DBPROP_DELAYSTORAGEOBJECTS|
|向后提取|DBPROP_CANFETCHBACKWARDS|
|保留行|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|固定行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IrowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch|DBPROP_IRowsetResynch|
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
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
|输出编码属性|DBPROP_OUTPUTENCODING|
|Output Stream 属性|DBPROP_OUTPUTSTREAM|
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
|服务器游标|DBPROP_SERVERCURSOR|
|服务器在插入数据|DBPROP_SERVERDATAONINSERT|
|跳过删除的书签|DBPROP_BOOKMARKSKIP|
|强行标识|DBPROP_STRONGIDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用书签|DBPROP_BOOKMARKS|
|XML 根|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 有关特定的实现详细信息和有关 Microsoft SQL Server OLE DB 提供程序的功能信息，请参阅[SQL Server 提供程序](https://msdn.microsoft.com/adf1d6c4-5930-444a-9248-ff1979729635)。

## <a name="see-also"></a>请参阅
 [ConnectionString 属性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [提供程序属性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
