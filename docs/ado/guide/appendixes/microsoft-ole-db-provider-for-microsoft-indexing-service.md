---
title: Microsoft OLE DB Provider for Microsoft 索引服务 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f84d13fa3f4e2da728c914f2228233a04e64643f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Microsoft OLE DB Provider for Microsoft 索引服务概述
Microsoft OLE DB Provider for Microsoft 索引服务提供编程的只读访问，以文件系统和 Web 数据由 Microsoft 索引服务编制索引。 ADO 应用程序可以发出 SQL 查询以检索内容和文件属性信息。

 该提供程序是自由线程和启用 UNICODE。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到此提供程序，设置**提供程序 =**参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性：

```
MSIDXS
```

 读取[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性将返回此字符串以及。

## <a name="typical-connection-string"></a>典型的连接字符串
 此提供程序的典型连接字符串是：

```
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 该字符串包含这些关键字：

|关键字|Description|
|-------------|-----------------|
|**提供程序**|指定 Microsoft 索引服务的 OLE DB 访问接口。 通常，这是连接字符串中指定的唯一一个关键字。|
|**数据源**|指定的索引服务目录名称。 如果未指定此关键字，则使用默认系统目录。|
|**区域设置标识符**|指定唯一的 32 位数字 （例如 1033年），指定与用户的语言首选项。 如果未指定此关键字，则使用默认系统区域设置标识符。|

## <a name="command-text"></a>命令文本
 索引服务 SQL 查询语法包含 SQL 92 扩展**选择**语句并将其**FROM**和**其中**子句。 通过 OLE DB 行集，这可以使用 ADO 和作为操作返回查询的结果[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。

 你可以搜索完全匹配的字词或短语，或使用通配符来搜索的模式或单词的词干。 搜索逻辑可以基于布尔决策、 加权的词或与其他单词的邻近。 您还可以搜索由"自定义文本，"查找根据含义，而不是完全匹配的字词进行匹配。

 特定命令方言完全记录在索引服务文档查询语言中。

 提供程序不接受存储的过程调用或简单的表名称 (例如， [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性将始终为**adCmdText**)。

## <a name="recordset-behavior"></a>记录集行为
 下表列出了提供的功能**记录集**对象打开到此提供程序。 只有静态游标类型 (**adOpenStatic**) 可用。

 有关详细信息有关**记录集**行为你提供程序配置，运行[支持](../../../ado/reference/ado-api/supports-method.md)方法和枚举[属性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合**记录集**以确定是否存在特定于提供程序的动态属性。

 **标准 ADO 记录集属性的可用性：**

|属性|可用性|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|读/写|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|读/写|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|只读|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|只读|
|[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)*|读/写|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|读/写|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|始终**adUseServer**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|始终**adOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|始终**adEditNone**|
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|只读|
|[筛选](../../../ado/reference/ado-api/filter-property.md)|读/写|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|读/写|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|不可用|
|[最大记录](../../../ado/reference/ado-api/maxrecords-property-ado.md)|读/写|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|只读|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|读/写|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|只读|
|[数据源](../../../ado/reference/ado-api/source-property-ado-recordset.md)|读/写|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|只读|
|[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)|只读|

 \*为了使此功能中的提供程序上存在，必须启用书签**记录集**。

 **标准 ADO 记录集方法的可用性：**

|方法|可用？|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|否|
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|是|
|[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|否|
|[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|否|
|[克隆](../../../ado/reference/ado-api/clone-method-ado.md)|是|
|[关闭](../../../ado/reference/ado-api/close-method-ado.md)|是|
|[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|否|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|是|
|[“移动”](../../../ado/reference/ado-api/move-method-ado.md)|是|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|是|
|[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)|是|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|是|
|[重新同步](../../../ado/reference/ado-api/resync-method.md)|是|
|[支持](../../../ado/reference/ado-api/supports-method.md)|是|
|[更新](../../../ado/reference/ado-api/update-method.md)|否|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|否|

 有关特定的实现详细信息和 Microsoft 索引服务 Microsoft OLE DB 提供程序的功能信息，请查阅[OLE DB 程序员指南](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx)，或访问 Windows NT Server Web 的 Web 服务页站点。

## <a name="see-also"></a>另请参阅
 [CommandType 属性 (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md) [ConnectionString 属性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [提供程序属性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [支持方法](../../../ado/reference/ado-api/supports-method.md)
