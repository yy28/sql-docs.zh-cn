---
title: 用于 Microsoft 索引服务的 Microsoft OLE DB 提供程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: dea7ec95efc1f560a2279868b2116d02d7ad6fef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701203"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Microsoft OLE DB Provider for Microsoft 索引服务概述
Microsoft OLE DB 访问接口用于 Microsoft 索引服务提供编程的只读访问，以文件系统和 Web 数据由 Microsoft 索引服务编制索引。 ADO 应用程序可以发出 SQL 查询来检索内容和文件属性信息。

 提供程序是自由线程，支持 UNICODE。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到此提供程序，请设置**提供程序 =** 自变量[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性设置为：

```vb
MSIDXS
```

 读取[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性将返回此字符串的形式。

## <a name="typical-connection-string"></a>典型的连接字符串
 此提供程序的典型的连接字符串是：

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 该字符串包含这些关键字：

|关键字|Description|
|-------------|-----------------|
|**提供程序**|指定用于 Microsoft 索引服务的 OLE DB 访问接口。 这通常是连接字符串中指定的唯一一个关键字。|
|**数据源**|指定的索引服务目录名称。 如果未指定此关键字，则使用默认系统目录。|
|**区域设置标识符**|指定唯一的 32 位数字 （例如 1033年），指定与用户的语言首选项。 如果未指定此关键字，则使用默认的系统区域设置标识符。|

## <a name="command-text"></a>命令文本
 索引服务 SQL 查询语法包含扩展到 SQL-92**选择**语句并将其**FROM**并**其中**子句。 通过 OLE DB 行集，这可以使用 ADO 和操作以返回查询的结果[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。

 您可以搜索完全匹配的字词或短语，或使用通配符搜索模式或单词的词干。 搜索逻辑可以基于布尔决策、 加权的词或靠近其他单词。 此外可以通过"自定义文本，"查找匹配基于的含义，而不是完全匹配的字词进行搜索。

 将特定命令方言完全记录在索引服务文档的查询语言。

 提供程序不接受简单的表名称或存储的过程调用 (例如， [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性将始终为**adCmdText**)。

## <a name="recordset-behavior"></a>记录集行为
 下表列出了可用的功能**记录集**对象打开与此提供程序。 只有静态游标类型 (**adOpenStatic**) 可用。

 有关更多有关详细信息**记录集**您运行的提供程序配置的行为[支持](../../../ado/reference/ado-api/supports-method.md)方法和枚举[属性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合**记录集**以确定是否存在特定于提供程序的动态属性。

 **标准的 ADO 记录集属性的可用性：**

|属性|可用性|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|read/write|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|read/write|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|只读|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|只读|
|[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)*|read/write|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|read/write|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|始终**adUseServer**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|always **adOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|始终**adEditNone**|
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|只读|
|[Filter](../../../ado/reference/ado-api/filter-property.md)|read/write|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|read/write|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|不可用|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|read/write|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|只读|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|read/write|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|只读|
|[数据源](../../../ado/reference/ado-api/source-property-ado-recordset.md)|read/write|
|[状态](../../../ado/reference/ado-api/state-property-ado.md)|只读|
|[“状态”](../../../ado/reference/ado-api/status-property-ado-recordset.md)|只读|

 \*必须存在于为了使此功能提供程序上启用书签**记录集**。

 **标准的 ADO 记录集方法的可用性：**

|方法|可用？|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|否|
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|是|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|否|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|否|
|[克隆](../../../ado/reference/ado-api/clone-method-ado.md)|是|
|[关闭](../../../ado/reference/ado-api/close-method-ado.md)|是|
|[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|否|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|是|
|[“移动”](../../../ado/reference/ado-api/move-method-ado.md)|是|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|是|
|[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)|是|
|[再次查询](../../../ado/reference/ado-api/requery-method.md)|是|
|[重新同步](../../../ado/reference/ado-api/resync-method.md)|是|
|[支持](../../../ado/reference/ado-api/supports-method.md)|是|
|[Update](../../../ado/reference/ado-api/update-method.md)|否|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|否|

 有关特定的实现详细信息和有关 Microsoft OLE DB 提供程序用于 Microsoft 索引服务的功能信息，请查阅[OLE DB 程序员指南](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx)，或访问 Windows NT Server Web 的 Web Services 页站点。

## <a name="see-also"></a>请参阅
 [CommandType 属性 (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md) [ConnectionString 属性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [提供程序属性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [支持方法](../../../ado/reference/ado-api/supports-method.md)
