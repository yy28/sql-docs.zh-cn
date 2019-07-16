---
title: Microsoft OLE DB Provider for ODBC |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for ODBC [ADO]
- providers [ADO], OLE DB provider for ODBC
ms.assetid: 2dc0372d-e74d-4d0f-9c8c-04e5a168c148
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25db7fdb20ceb2dd24f819e1db7077d40f7e7e3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926639"
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Microsoft OLE DB Provider for ODBC 概述
到 ADO 或 RDS 的程序员来说，理想情况下将是一个中的每个数据源公开 OLE DB 接口，以便 ADO 无法直接调用到数据源。 尽管越来越多的数据库供应商实现 OLE DB 接口，但某些数据源是尚未公开这种方式。 但是，可以通过 ODBC 访问大多数系统 （DBMS） 目前所用。

 可用于每个主要 DBMS 当今，使用非 Microsoft 数据库产品，例如 Oracle 除了包括 Microsoft SQL Server、 Microsoft Access （Microsoft Jet 数据库引擎） 和 Microsoft FoxPro ODBC 驱动程序。

 Microsoft ODBC 提供程序，但是，允许 ADO 连接到任何 ODBC 数据源。 提供程序是自由线程，支持 Unicode。

 提供程序支持事务，尽管不同的 DBMS 引擎提供了不同类型的事务支持。 例如，Microsoft Access 支持最多五个级别的嵌套的事务。

 这是 ADO 的默认提供程序，支持所有依赖于访问接口的 ADO 属性和方法。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到此提供程序，请设置**提供程序 =** 的参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性设置为：

```
MSDASQL
```

 读取[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性将返回此字符串的形式。

## <a name="typical-connection-string"></a>典型的连接字符串
 此提供程序的典型的连接字符串是：

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 该字符串包含这些关键字：

|关键字|描述|
|-------------|-----------------|
|**提供程序**|指定用于 ODBC 的 OLE DB 访问接口。|
|**DSN**|指定数据源名称。|
|**UID**|指定用户名称。|
|**PWD**|指定用户密码。|
|**URL**|指定的文件或目录已发布的 Web 文件夹中的 URL。|

 由于这是默认的提供程序用于 ADO 中，如果省略**提供程序 =** 将参数从连接字符串，ADO 将尝试建立与此提供程序的连接。

> [!NOTE]
>  如果您要连接到的数据源提供程序支持 Windows 身份验证，则应指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是用户 ID 和密码在连接字符串中的信息。

 提供程序不支持除 ADO 定义的任何特定的连接参数。 但是，该提供程序会将任何非 ADO 连接参数传递到 ODBC 驱动程序管理器。

 因为可以省略**提供程序**参数，可以因此编写等同于同一数据源的 ODBC 连接字符串的 ADO 连接字符串。 使用相同的参数名称 (**驱动程序 =** ，**数据库 =** ， **DSN =** ，依此类推)，值和与您的语法将撰写的 ODBC 连接字符串时。 可以带或不带预定义的数据源名称 (DSN) 或 FileDSN 连接。

## <a name="syntax-with-a-dsn-or-filedsn"></a>使用 DSN 或 FileDSN 语法：

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>没有 DSN （无 DSN 连接） 的语法：

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>备注
 如果您使用**DSN**或**FileDSN**，必须定义通过 ODBC 数据源管理器在 Windows 控制面板中。 在 Microsoft Windows 2000 中，ODBC 管理器位于管理工具。 在早期版本的 Windows 中，名为 ODBC 管理器图标**32 位 ODBC**或仅**ODBC**。

 作为设置的替代方法**DSN**，可以指定 ODBC 驱动程序 (**驱动程序 =** )，例如"SQL Server;"服务器名称 (**SERVER =** ); 和数据库名称 (**数据库 =** )。

 此外可以指定用户帐户名 (**UID =** )，以及用户帐户的密码 (**PWD =** ) 中的特定于 ODBC 的参数或在标准 ADO 定义*用户*和*密码*参数。

 尽管**DSN**定义中已指定了数据库，您可以指定  *数据库*除了参数**DSN**连接到不同的数据库。 它是始终包含一个好办法  *数据库*时使用的参数**DSN**。 这将确保您连接到正确的数据库的，如果自上次检查时间，另一个用户更改了默认的数据库参数**DSN**定义。

## <a name="provider-specific-connection-properties"></a>特定于提供程序的连接属性
 用于 ODBC 的 OLE DB 访问接口将添加到多个属性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)系列**连接**对象。 下表列出了这些属性与在括号中相应的 OLE DB 属性名称。

|属性名|描述|
|-------------------|-----------------|
|可访问的过程 (KAGPROP_ACCESSIBLEPROCEDURES)|指示用户是否有权访问的存储过程。|
|可访问的表 (KAGPROP_ACCESSIBLETABLES)|指示用户是否具有执行针对数据库表的 SELECT 语句的权限。|
|活动语句 (KAGPROP_ACTIVESTATEMENTS)|指示句柄 ODBC 驱动程序可以在连接支持的数量。|
|驱动程序名称 (KAGPROP_DRIVERNAME)|指示 ODBC 驱动程序的文件名称。|
|驱动程序的 ODBC 版本 (KAGPROP_DRIVERODBCVER)|指示此驱动程序支持 ODBC 的版本。|
|文件使用情况 (KAGPROP_FILEUSAGE)|指示如何驱动程序会将数据源; 中的文件为表或为编录。|
|Like 转义子句 (KAGPROP_LIKEESCAPECLAUSE)|指示是否该驱动程序支持的定义和转义字符的使用百分比字符 （%）和 WHERE 子句在 LIKE 谓词中下划线字符 (_)。|
|分组依据 (KAGPROP_MAXCOLUMNSINGROUPBY) 中最大列数|指示可以在 SELECT 语句的 GROUP BY 子句中列出的列的最大数目。|
|索引 (KAGPROP_MAXCOLUMNSININDEX) 中最大列数|指示列可以包含在索引中的最大数目。|
|在排序依据 (KAGPROP_MAXCOLUMNSINORDERBY) 最大列数|指示可以在 SELECT 语句的 ORDER BY 子句中列出的列的最大数目。|
|在中，选择 (KAGPROP_MAXCOLUMNSINSELECT) 最大列数|指示可以在 SELECT 语句的 SELECT 部分中列出的列的最大数目。|
|表 (KAGPROP_MAXCOLUMNSINTABLE) 中最大列数|指示列在表中允许的最大数目。|
|数值函数 (KAGPROP_NUMERICFUNCTIONS)|指示 ODBC 驱动程序支持的数值的函数。 函数名称和此位掩码中使用的关联的值的列表，请参阅[附录 e:标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文档中。|
|外部联接功能 (KAGPROP_OJCAPABILITY)|指示提供程序支持外部联接的类型。|
|外部联接 (KAGPROP_OUTERJOINS)|指示提供程序是否支持外部联接。|
|特殊字符 (KAGPROP_SPECIALCHARACTERS)|指示哪些字符具有特殊含义的 ODBC 驱动程序。|
|存储的过程 (KAGPROP_PROCEDURES)|指示存储的过程是否可与此 ODBC 驱动程序一起使用。|
|字符串函数 (KAGPROP_STRINGFUNCTIONS)|指示 ODBC 驱动程序支持的字符串函数。 函数名称和此位掩码中使用的关联的值的列表，请参阅[附录 e:标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文档中。|
|系统函数 (KAGPROP_SYSTEMFUNCTIONS)|指示 ODBC 驱动程序支持的系统函数。 函数名称和此位掩码中使用的关联的值的列表，请参阅[附录 e:标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文档中。|
|时间/日期函数 (KAGPROP_TIMEDATEFUNCTIONS)|指示 ODBC 驱动程序支持的日期和时间函数。 函数名称和此位掩码中使用的关联的值的列表，请参阅[附录 e:标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文档中。|
|SQL 语法支持 (KAGPROP_ODBCSQLCONFORMANCE)|指示 ODBC 驱动程序支持的 SQL 语法。|

## <a name="provider-specific-recordset-and-command-properties"></a>特定于提供程序的记录集和命令属性
 用于 ODBC 的 OLE DB 访问接口将添加到多个属性**属性**系列**记录集**并**命令**对象。 下表列出了这些属性与在括号中相应的 OLE DB 属性名称。

|属性名|描述|
|-------------------|-----------------|
|基于查询的更新/删除/插入 (KAGPROP_QUERYBASEDUPDATES)|指示是否可以通过使用 SQL 查询执行更新、 删除和插入操作。|
|ODBC 并发类型 (KAGPROP_CONCURRENCY)|指示用于减少可能导致两个用户尝试从数据源同时访问同一数据的问题的方法。|
|只进游标 (KAGPROP_BLOBSONFOCURSOR) 上的 BLOB 可访问性|指示是否 BLOB**字段**使用只进游标时可访问。|
|SQL_FLOAT、 SQL_DOUBLE 和 SQL_REAL 纳入 QBU WHERE 子句 (KAGPROP_INCLUDENONEXACT)|指示是否可以在其中 QBU 子句中包含 SQL_FLOAT、 SQL_DOUBLE 和 SQL_REAL 值。|
|插入 (KAGPROP_POSITIONONNEWROW) 后的最后一行上的位置|指示已在表中插入一条新记录后，将为表中的最后一行来自当前行。|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|指示是否**IRowsetChange**接口提供的扩展的信息的支持。|
|ODBC 游标类型 (KAGPROP_CURSOR)|指示使用的游标的类型**记录集**。|
|生成行集可以封送 (KAGPROP_MARSHALLABLE)|指示 ODBC 驱动程序生成的记录集，可以进行封送处理|

## <a name="command-text"></a>命令文本
 如何使用[命令](../../../ado/reference/ado-api/command-object-ado.md)对象很大程度上取决于数据源，并将接受查询或命令语句的类型。

 ODBC 提供了用于调用存储的过程的特定语法。 有关[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)的属性**命令**对象， *CommandText*参数**Execute**方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，或*源*自变量**打开**方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，此语法将字符串中传递：

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , ... ]] ) ] }"
```

 每个 **？** 引用中的对象[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 第一个 **？** 引用**参数**(0)，下一步 **？** 引用**参数**(1)，依此类推。

 参数引用是可选的取决于存储过程的结构。 如果你想要调用未定义任何参数的存储的过程，您的字符串将如下所示如下：

```
"{ call procedure }"
```

 如果您有两个查询参数，您的字符串将如下所示：

```
"{ call procedure ( ?, ? ) }"
```

 如果存储的过程将返回一个值，则返回值视为另一个参数。 如果不有任何查询参数，但必须返回值，您的字符串将如下所示：

```
"{ ? = call procedure }"
```

 最后，如果返回值，并且两个查询参数，您的字符串将如下所示：

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>记录集行为
 下表列出了标准的 ADO 方法和属性可在上找到**记录集**对象打开与此提供程序。

 有关更多有关详细信息**记录集**您运行的提供程序配置的行为[支持](../../../ado/reference/ado-api/supports-method.md)方法和枚举**属性**的集合**记录集**以确定是否存在特定于提供程序的动态属性。

 可用性标准 ADO**记录集**属性：

|属性|ForwardOnly|动态|Keyset|Static|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|不可用|不可用|读/写|读/写|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|不可用|不可用|读/写|读/写|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|读/写|读/写|读/写|读/写|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|只读|只读|只读|只读|
|[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)|不可用|不可用|读/写|读/写|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|读/写|读/写|读/写|读/写|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|读/写|读/写|读/写|读/写|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|读/写|读/写|读/写|读/写|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|只读|只读|只读|只读|
|[Filter](../../../ado/reference/ado-api/filter-property.md)|读/写|读/写|读/写|读/写|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|读/写|读/写|读/写|读/写|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|读/写|读/写|读/写|读/写|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|读/写|读/写|读/写|读/写|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|读/写|不可用|只读|只读|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|读/写|读/写|读/写|读/写|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|读/写|不可用|只读|只读|
|[数据源](../../../ado/reference/ado-api/source-property-ado-recordset.md)|读/写|读/写|读/写|读/写|
|[状态](../../../ado/reference/ado-api/state-property-ado.md)|只读|只读|只读|只读|
|[“状态”](../../../ado/reference/ado-api/status-property-ado-recordset.md)|只读|只读|只读|只读|

 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)并[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)属性是只写 ADO 用于 ODBC 的 1.0 版的 Microsoft OLE DB 访问接口时。

 可用性标准 ADO**记录集**方法：

|方法|ForwardOnly|动态|Keyset|Static|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|是|是|是|是|
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|是|是|是|是|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|是|是|是|是|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|是|是|是|是|
|[克隆](../../../ado/reference/ado-api/clone-method-ado.md)|否|否|是|是|
|[关闭](../../../ado/reference/ado-api/close-method-ado.md)|是|是|是|是|
|[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|是|是|是|是|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|是|是|是|是|
|[“移动”](../../../ado/reference/ado-api/move-method-ado.md)|是|是|是|是|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|是|是|是|
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|否|是|是|是|
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|是|是|是|
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|否|是|是|是|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)*|是|是|是|是|
|[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)|是|是|是|是|
|[再次查询](../../../ado/reference/ado-api/requery-method.md)|是|是|是|是|
|[重新同步](../../../ado/reference/ado-api/resync-method.md)|否|否|是|是|
|[支持](../../../ado/reference/ado-api/supports-method.md)|是|是|是|是|
|[Update](../../../ado/reference/ado-api/update-method.md)|是|是|是|是|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|是|是|是|是|

 \* 不受支持的 Microsoft Access 数据库。

## <a name="dynamic-properties"></a>动态属性
 Microsoft OLE DB Provider for ODBC 将插入到多个动态属性**属性**的未打开集合[连接](../../../ado/reference/ado-api/connection-object-ado.md)，[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，以及[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。

 下表是 ADO 和 OLE DB 名称的每个动态属性的交叉索引。 OLE DB 程序员参考指 ADO 属性名称，术语"Description"。 在 OLE DB 程序员参考中，可以找到有关这些属性的详细信息。 搜索索引中的 OLE DB 属性名称，或参阅[附录 c:OLE DB 属性](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292)。

## <a name="connection-dynamic-properties"></a>连接的动态属性
 以下属性添加到**连接**对象的**属性**集合。

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
|Location|DBPROP_INIT_LOCATION|
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
|OLE DB 服务|DBPROP_INIT_OLEDBSERVICES|
|OLE DB 版本|DBPROP_PROVIDEROLEDBVER|
|OLE 对象支持|DBPROP_OLEOBJECTS|
|打开行集合支持|DBPROP_OPENROWSETSUPPORT|
|按选择列表中的列进行排序|DBPROP_ORDERBYCOLUMNSINSELECT|
|输出参数可用性|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Password|DBPROP_AUTH_PASSWORD|
|传递 By Ref 访问器|DBPROP_BYREFACCESSORS|
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
 以下属性添加到**记录集**对象的**属性**集合。

|ADO 属性名称|OLE DB 属性名|
|-----------------------|--------------------------|
|访问顺序|DBPROP_ACCESSORDER|
|模块化存储对象|DBPROP_BLOCKINGSTORAGEOBJECTS|
|书签类型|DBPROP_BOOKMARKTYPE|
|可存为书签|DBPROP_IROWSETLOCATE|
|更改插入的行|DBPROP_CHANGEINSERTEDROWS|
|列权限|DBPROP_COLUMNRESTRICT|
|列设置通知|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|唯一行|DBPROP_UNIQUEROWS|
|可更新性|DBPROP_UPDATABILITY|
|使用书签|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令动态属性
 以下属性添加到**命令**对象的**属性**集合。

|ADO 属性名称|OLE DB 属性名|
|-----------------------|--------------------------|
|访问顺序|DBPROP_ACCESSORDER|
|模块化存储对象|DBPROP_BLOCKINGSTORAGEOBJECTS|
|书签类型|DBPROP_BOOKMARKTYPE|
|可存为书签|DBPROP_IROWSETLOCATE|
|更改插入的行|DBPROP_CHANGEINSERTEDROWS|
|列权限|DBPROP_COLUMNRESTRICT|
|列设置通知|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|跳过删除的书签|DBPROP_BOOKMARKSKIP|
|强行标识|DBPROP_STRONGIDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用书签|DBPROP_BOOKMARKS|

 有关特定的实现和有关 Microsoft OLE DB 提供程序用于 ODBC 的功能信息的详细信息，请参阅[OLE DB 程序员参考](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)或访问 MSDN 上的数据访问和存储开发人员中心网站。

## <a name="see-also"></a>请参阅
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md) [CommandText 属性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [ConnectionString 属性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [执行方法 （ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md) [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md) [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md) [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [提供程序属性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [支持方法](../../../ado/reference/ado-api/supports-method.md)
