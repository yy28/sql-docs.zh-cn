---
title: "Microsoft OLE DB Provider for ODBC |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB provider for ODBC [ADO]
- providers [ADO], OLE DB provider for ODBC
ms.assetid: 2dc0372d-e74d-4d0f-9c8c-04e5a168c148
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 44f3131bff34d35b334495c7c718eb513f5d88bf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Microsoft OLE DB Provider for ODBC 概述
到 ADO 或 RDS 的程序员来说，理想情况下将是一个中的每个数据源公开 OLE DB 接口，以便 ADO 无法直接调入数据源。 尽管越来越多的数据库供应商实现 OLE DB 接口，但某些数据源不尚未公开这种方式。 但是，可以通过 ODBC 访问当今使用的大多数 DBMS 系统。

 ODBC 驱动程序都可用于诸如 Oracle 等的非 Microsoft 的数据库产品除了包括 Microsoft SQL Server、 Microsoft Access （Microsoft Jet 数据库引擎） 和 Microsoft FoxPro，目前，所用每个主要 DBMS。

 Microsoft ODBC 访问接口，但是，允许 ADO 连接到任何 ODBC 数据源。 该提供程序是自由线程和启用 Unicode。

 提供程序支持事务，但不同 DBMS 引擎提供了不同类型的事务支持。 例如，Microsoft Access 支持最多五个级别深层嵌套的事务。

 这是默认提供程序 ADO，并支持所有依赖于提供程序的 ADO 属性和方法。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到此提供程序，设置**提供程序 =**参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性：

```
MSDASQL
```

 读取[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性将返回此字符串以及。

## <a name="typical-connection-string"></a>典型的连接字符串
 此提供程序的典型连接字符串是：

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 该字符串包含这些关键字：

|关键字|Description|
|-------------|-----------------|
|**提供程序**|指定适用于 ODBC 的 OLE DB 访问接口。|
|**DSN**|指定数据源名称。|
|**UID**|指定的用户名。|
|**PWD**|指定的用户密码。|
|**URL**|指定的文件或目录中的 Web 文件夹发布的 URL。|

 因为这是默认提供程序 ADO，如果省略**提供程序 =**参数从连接字符串，ADO 将尝试建立与此提供程序的连接。

> [!NOTE]
>  如果你要连接到的数据源提供程序支持 Windows 身份验证，你应指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是用户 ID 和密码连接字符串中的信息。

 提供程序不支持除 ADO 定义的任何特定的连接参数。 但是，该提供程序会将任何非 ADO 连接参数传递到 ODBC 驱动程序管理器。

 因为可以省略**提供程序**参数，可以因此撰写等同于同一数据源将 ODBC 连接字符串的 ADO 连接字符串。 使用相同的参数名 (**驱动程序 =**，**数据库 =**， **DSN =**，依次类推)，值和为你的语法将撰写 ODBC 连接字符串时。 你可以连接和不带预定义的数据源名称 (DSN) 或 FileDSN。

## <a name="syntax-with-a-dsn-or-filedsn"></a>与 DSN 或 FileDSN 语法：

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>没有 DSN （dsn 连接） 的语法：

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>Remarks
 如果你使用**DSN**或**FileDSN**，必须定义通过 ODBC 数据源管理器在 Windows 控制面板中。 在 Microsoft Windows 2000 中，ODBC 管理器位于管理工具。 在早期版本的 Windows 中，名为 ODBC 管理器图标**32 位 ODBC**或仅仅称为**ODBC**。

 作为设置的替代方法**DSN**，你可以指定的 ODBC 驱动程序 (**驱动程序 =**)，例如"SQL Server;"服务器名称 (**SERVER =**); 和数据库名称 (**数据库 =**)。

 你还可以指定一个用户帐户名 (**UID =**)，以及用户帐户的密码 (**PWD =**) 中的特定于 ODBC 的参数或标准中 ADO 定义*用户*和*密码*参数。

 尽管**DSN**定义已指定了数据库，你可以指定 *数据库*除了参数**DSN**连接到不同的数据库。 它是始终包含一个好办法 *数据库*参数，当你使用**DSN**。 这将确保你连接到正确的数据库的，如果自上次检查以来，另一个用户更改默认数据库参数**DSN**定义。

## <a name="provider-specific-connection-properties"></a>提供程序特定的连接属性
 适用于 ODBC 的 OLE DB 访问接口将添加到多个属性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合**连接**对象。 下表列出在括号中对应的 OLE DB 属性名具有这些属性。

|属性名称|Description|
|-------------------|-----------------|
|可访问的过程 (KAGPROP_ACCESSIBLEPROCEDURES)|指示用户是否有权访问的存储过程。|
|可访问的表 (KAGPROP_ACCESSIBLETABLES)|指示用户是否具有执行针对数据库表的 SELECT 语句的权限。|
|活动语句 (KAGPROP_ACTIVESTATEMENTS)|指示 ODBC 驱动程序可以在连接支持的句柄数。|
|驱动程序名称 (KAGPROP_DRIVERNAME)|指示 ODBC 驱动程序的文件名称。|
|驱动程序的 ODBC 版本 (KAGPROP_DRIVERODBCVER)|指示此驱动程序支持的 ODBC 版本。|
|文件使用情况 (KAGPROP_FILEUSAGE)|指示该驱动程序如何处理数据源; 中的文件为表或为编录。|
|如 Escape 子句 (KAGPROP_LIKEESCAPECLAUSE)|WHERE 子句的 LIKE 谓词中，该值指示是否驱动程序支持的定义和使用转义符的百分比字符 （%） 和下划线字符 (_)。|
|在组中按 (KAGPROP_MAXCOLUMNSINGROUPBY) 最大列数|指示最大可以 SELECT 语句的 GROUP BY 子句中列出的列数。|
|索引 (KAGPROP_MAXCOLUMNSININDEX) 中最大列数|表示可以包含在索引的列的最大数目。|
|在 Order By (KAGPROP_MAXCOLUMNSINORDERBY) 最大列数|指示最大可以 SELECT 语句的 ORDER BY 子句中列出的列数。|
|在选择 (KAGPROP_MAXCOLUMNSINSELECT) 最大列数|表示可以在 SELECT 语句的 SELECT 部分中列出的列的最大数目。|
|表 (KAGPROP_MAXCOLUMNSINTABLE) 中最大列数|指示最大允许表中的列数。|
|数值函数 (KAGPROP_NUMERICFUNCTIONS)|指示 ODBC 驱动程序支持的数值的函数。 函数名称和此位掩码中使用的关联的值的列表，请参阅[附录 e： 标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文档中。|
|外部联接功能 (KAGPROP_OJCAPABILITY)|指示的提供程序支持外部联接的类型。|
|外部联接 (KAGPROP_OUTERJOINS)|指示提供程序是否支持外部联接。|
|特殊字符 (KAGPROP_SPECIALCHARACTERS)|指示哪些字符具有特殊含义的 ODBC 驱动程序。|
|存储的过程 (KAGPROP_PROCEDURES)|指示存储的过程是否可与此 ODBC 驱动程序一起使用。|
|字符串函数 (KAGPROP_STRINGFUNCTIONS)|指示 ODBC 驱动程序支持的字符串函数。 函数名称和此位掩码中使用的关联的值的列表，请参阅[附录 e： 标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文档中。|
|系统函数 (KAGPROP_SYSTEMFUNCTIONS)|指示 ODBC 驱动程序支持的系统函数。 函数名称和此位掩码中使用的关联的值的列表，请参阅[附录 e： 标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文档中。|
|时间/日期函数 (KAGPROP_TIMEDATEFUNCTIONS)|指示 ODBC 驱动程序支持的日期和时间函数。 函数名称和此位掩码中使用的关联的值的列表，请参阅[附录 e： 标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文档中。|
|SQL 语法支持 (KAGPROP_ODBCSQLCONFORMANCE)|指示 ODBC 驱动程序支持的 SQL 语法。|

## <a name="provider-specific-recordset-and-command-properties"></a>提供程序特定的记录集和命令属性
 适用于 ODBC 的 OLE DB 访问接口将添加到多个属性**属性**集合**记录集**和**命令**对象。 下表列出在括号中对应的 OLE DB 属性名具有这些属性。

|属性名称|Description|
|-------------------|-----------------|
|基于查询的更新/删除/插入 (KAGPROP_QUERYBASEDUPDATES)|指示是否可以使用 SQL 查询执行更新、 删除和插入。|
|ODBC 并发类型 (KAGPROP_CONCURRENCY)|指示用于减少通过尝试从数据源中同时访问相同的数据的两个用户而导致的潜在问题的方法。|
|只进游标 (KAGPROP_BLOBSONFOCURSOR) 上的 BLOB 可访问性|指示是否 BLOB**字段**使用只进游标时可以访问。|
|SQL_FLOAT、 SQL_DOUBLE 和 SQL_REAL 纳入 QBU WHERE 子句 (KAGPROP_INCLUDENONEXACT)|指示是否可以为 QBU WHERE 子句包含 SQL_FLOAT、 SQL_DOUBLE 和 SQL_REAL 值。|
|在最后一行后插入 (KAGPROP_POSITIONONNEWROW) 的位置|指示已在表中插入一条新记录后，将会在表中的最后一行来自当前行。|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|指示是否**IRowsetChange**接口支持扩展的信息。|
|ODBC 游标类型 (KAGPROP_CURSOR)|指示的游标由类型**记录集**。|
|生成行集可以进行封送处理 (KAGPROP_MARSHALLABLE)|指示 ODBC 驱动程序生成的记录集可以进行封送处理|

## <a name="command-text"></a>命令文本
 如何使用[命令](../../../ado/reference/ado-api/command-object-ado.md)对象很大程度上取决于数据源，而且也会接受哪种类型的查询或命令语句。

 ODBC 提供特定的语法来调用存储的过程。 有关[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性**命令**对象， *CommandText*参数**执行**方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，或*源*参数**打开**方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，使用以下语法字符串中传递：

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , … ]] ) ] }"
```

 每个**？** 引用中的对象[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 第一个**？** 引用**参数**(0)，下一步**？** 引用**参数**(1)，依次类推。

 参数引用是可选的取决于存储过程的结构。 如果你想要调用存储的过程定义没有参数，则字符串将类似以下：

```
"{ call procedure }"
```

 如果你有两个查询参数，你的字符串将如下所示：

```
"{ call procedure ( ?, ? ) }"
```

 如果存储的过程将返回一个值，则返回值视为另一个参数。 如果你有任何查询参数，但必须返回值，你的字符串将如下所示：

```
"{ ? = call procedure }"
```

 最后，如果你有一个返回值，并且两个查询参数，你的字符串将如下所示：

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>记录集行为
 下表列出的标准 ADO 方法和属性上可用**记录集**对象打开到此提供程序。

 有关详细信息有关**记录集**行为你提供程序配置，运行[支持](../../../ado/reference/ado-api/supports-method.md)方法和枚举**属性**的集合**记录集**以确定是否存在特定于提供程序的动态属性。

 标准 ADO 可用性**记录集**属性：

|“属性”|ForwardOnly|Dynamic|Keyset|静态|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|不可用|不可用|读/写|读/写|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|不可用|不可用|读/写|读/写|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|读/写|读/写|读/写|读/写|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|只读|只读|只读|只读|
|[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)|不可用|不可用|读/写|读/写|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|读/写|读/写|读/写|读/写|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|读/写|读/写|读/写|读/写|
|[游标类型](../../../ado/reference/ado-api/cursortype-property-ado.md)|读/写|读/写|读/写|读/写|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|只读|只读|只读|只读|
|[Filter](../../../ado/reference/ado-api/filter-property.md)|读/写|读/写|读/写|读/写|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|读/写|读/写|读/写|读/写|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|读/写|读/写|读/写|读/写|
|[最大记录](../../../ado/reference/ado-api/maxrecords-property-ado.md)|读/写|读/写|读/写|读/写|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|读/写|不可用|只读|只读|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|读/写|读/写|读/写|读/写|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|读/写|不可用|只读|只读|
|[数据源](../../../ado/reference/ado-api/source-property-ado-recordset.md)|读/写|读/写|读/写|读/写|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|只读|只读|只读|只读|
|[“状态”](../../../ado/reference/ado-api/status-property-ado-recordset.md)|只读|只读|只读|只读|

 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)和[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)属性是只写，如果 ADO 用于用于 ODBC 的 Microsoft OLE DB 提供程序的 1.0 版。

 标准 ADO 可用性**记录集**方法：

|方法|ForwardOnly|Dynamic|Keyset|静态|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|是|是|是|是|
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|是|是|是|是|
|[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|是|是|是|是|
|[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|是|是|是|是|
|[克隆](../../../ado/reference/ado-api/clone-method-ado.md)|是|是|是|是|
|[关闭](../../../ado/reference/ado-api/close-method-ado.md)|是|是|是|是|
|[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|是|是|是|是|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|是|是|是|是|
|[“移动”](../../../ado/reference/ado-api/move-method-ado.md)|是|是|是|是|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|是|是|是|
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|是|是|是|
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|是|是|是|
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|是|是|是|
|[签名](../../../ado/reference/ado-api/nextrecordset-method-ado.md)*|是|是|是|是|
|[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)|是|是|是|是|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|是|是|是|是|
|[重新同步](../../../ado/reference/ado-api/resync-method.md)|是|是|是|是|
|[支持](../../../ado/reference/ado-api/supports-method.md)|是|是|是|是|
|[Update](../../../ado/reference/ado-api/update-method.md)|是|是|是|是|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|是|是|是|是|

 * 中不受支持的 Microsoft Access 数据库。

## <a name="dynamic-properties"></a>动态属性
 Microsoft OLE DB Provider for ODBC 插入到多个动态属性**属性**集合的未打开[连接](../../../ado/reference/ado-api/connection-object-ado.md)，[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，和[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。

 下表是每个动态属性的 ADO 和 OLE DB 名称交叉。 OLE DB 程序员参考指 ADO 属性名称，术语"Description"。 OLE DB 程序员参考中，你可以找到有关这些属性的详细信息。 搜索索引中的 OLE DB 属性名称，或请参阅[附录 c: OLE DB 属性](http://msdn.microsoft.com/en-us/deded3ff-f508-4e1b-b2b1-fd9afd3bd292)。

## <a name="connection-dynamic-properties"></a>连接的动态属性
 以下属性添加到**连接**对象的**属性**集合。

|ADO 属性名称|OLE DB 属性名称|
|-----------------------|--------------------------|
|活动会话|DBPROP_ACTIVESESSIONS|
|异步终止|DBPROP_ASYNCTXNABORT|
|可异步提交|DBPROP_ASYNCTNXCOMMIT|
|自动提交隔离级别|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|目录位置|DBPROP_CATALOGLOCATION|
|目录术语|DBPROP_CATALOGTERM|
|列定义|DBPROP_COLUMNDEFINITION|
|连接超时值|DBPROP_INIT_TIMEOUT|
|当前目录|DBPROP_CURRENTCATALOG|
|数据源|DBPROP_INIT_DATASOURCE|
|数据源名称|DBPROP_DATASOURCENAME|
|线程处理模型的数据源对象|DBPROP_DSOTHREADMODEL|
|DBMS 名称|DBPROP_DBMSNAME|
|DBMS 版本|DBPROP_DBMSVER|
|扩展的属性|DBPROP_INIT_PROVIDERSTRING|
|按支持进行分组|DBPROP_GROUPBY|
|异类表支持|DBPROP_HETEROGENEOUSTABLES|
|标识符区分大小写|DBPROP_IDENTIFIERCASE|
|初始目录|DBPROP_INIT_CATALOG|
|隔离级别|DBPROP_SUPPORTEDTXNISOLEVELS|
|隔离保留|DBPROP_SUPPORTEDTXNISORETAIN|
|区域设置标识符|DBPROP_INIT_LCID|
|位置|DBPROP_INIT_LOCATION|
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
|OLE DB 服务|DBPROP_INIT_OLEDBSERVICES|
|OLE DB 版本|DBPROP_PROVIDEROLEDBVER|
|OLE 对象支持|DBPROP_OLEOBJECTS|
|打开行集支持|DBPROP_OPENROWSETSUPPORT|
|通过选择列表中的列进行排序|DBPROP_ORDERBYCOLUMNSINSELECT|
|输出参数可用性|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Password|DBPROP_AUTH_PASSWORD|
|通过 Ref 访问器|DBPROP_BYREFACCESSORS|
|持久性安全信息|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
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
 以下属性添加到**记录集**对象的**属性**集合。

|ADO 属性名称|OLE DB 属性名称|
|-----------------------|--------------------------|
|访问顺序|DBPROP_ACCESSORDER|
|阻止存储对象|DBPROP_BLOCKINGSTORAGEOBJECTS|
|书签类型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|更改插入的行|DBPROP_CHANGEINSERTEDROWS|
|列权限|DBPROP_COLUMNRESTRICT|
|列集通知|DBPROP_NOTIFYCOLUMNSET|
|延迟存储对象更新|DBPROP_DELAYSTORAGEOBJECTS|
|向后获取|DBPROP_CANFETCHBACKWARDS|
|保存行|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|固定的行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IrowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IrowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|文本书签|DBPROP_LITERALBOOKMARKS|
|文本行标识|DBPROP_LITERALIDENTITY|
|打开的最大行数|DBPROP_MAXOPENROWS|
|最大挂起行|DBPROP_MAXPENDINGROWS|
|最大行数|DBPROP_MAXROWS|
|通知粒度|DBPROP_NOTIFICATIONGRANULARITY|
|通知阶段|DBPROP_NOTIFICATIONPHASES|
|事务处理的对象|DBPROP_TRANSACTEDOBJECT|
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
|唯一行|DBPROP_UNIQUEROWS|
|可更新性|DBPROP_UPDATABILITY|
|使用书签|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令动态属性
 以下属性添加到**命令**对象的**属性**集合。

|ADO 属性名称|OLE DB 属性名称|
|-----------------------|--------------------------|
|访问顺序|DBPROP_ACCESSORDER|
|阻止存储对象|DBPROP_BLOCKINGSTORAGEOBJECTS|
|书签类型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|更改插入的行|DBPROP_CHANGEINSERTEDROWS|
|列权限|DBPROP_COLUMNRESTRICT|
|列集通知|DBPROP_NOTIFYCOLUMNSET|
|延迟存储对象更新|DBPROP_DELAYSTORAGEOBJECTS|
|向后获取|DBPROP_CANFETCHBACKWARDS|
|保存行|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|固定的行|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IrowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IrowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|文本书签|DBPROP_LITERALBOOKMARKS|
|文本行标识|DBPROP_LITERALIDENTITY|
|打开的最大行数|DBPROP_MAXOPENROWS|
|最大挂起行|DBPROP_MAXPENDINGROWS|
|最大行数|DBPROP_MAXROWS|
|通知粒度|DBPROP_NOTIFICATIONGRANULARITY|
|通知阶段|DBPROP_NOTIFICATIONPHASES|
|事务处理的对象|DBPROP_TRANSACTEDOBJECT|
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
|跳过删除书签|DBPROP_BOOKMARKSKIP|
|强行标识|DBPROP_STRONGIDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用书签|DBPROP_BOOKMARKS|

 有关特定实现和 ODBC Microsoft OLE DB 提供程序的功能信息的详细信息，请参阅[OLE DB 程序员参考](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)或访问 MSDN 上的数据访问和存储开发人员中心 Web 站点。

## <a name="see-also"></a>另请参阅
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md) [CommandText 属性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [ConnectionString 属性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [执行方法 （ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md) [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md) [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md) [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [提供程序属性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [支持方法](../../../ado/reference/ado-api/supports-method.md)
