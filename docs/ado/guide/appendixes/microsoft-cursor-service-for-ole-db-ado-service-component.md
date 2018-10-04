---
title: 用于 OLE DB （ADO 服务组件） 的 Microsoft 游标服务 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c859de289a9f93a23702c63bd50269bb0881b34
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47714985"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>用于 OLE DB 概述 Microsoft 游标服务
用于 OLE DB 的 Microsoft 游标服务补充数据访问接口的游标支持函数。 因此，用户可以体验从所有数据提供程序相对统一的功能。

 游标服务使动态属性可用，增强了某些方法的行为。 例如，[优化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)动态属性允许创建临时索引以简化某些操作，如[查找](../../../ado/reference/ado-api/find-method-ado.md)方法。

 游标服务支持批处理更新在所有情况下。 此外可以在数据访问接口仅提供性能较差的游标，如静态游标时模拟功能更强大的游标类型，如动态游标。

## <a name="keyword"></a>关键字
 若要调用此服务组件，请设置[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)或[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。

```
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>动态属性
 用于 OLE DB 游标服务调用时，将以下动态属性添加到**记录集**对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。 完整列表**连接**并**记录集**中列出对象动态属性[ADO 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)。 关联的 OLE DB 属性名称，在适当的情况是用括号括住的 ADO 属性名称。

 游标服务调用后，对某些动态属性的更改不到基础数据源可见。 例如，设置*命令超时*上的属性**记录集**不会对基础数据提供程序可见。

```

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 如果你的应用程序需要游标服务，但您需要在基础提供程序上设置动态属性，请调用游标服务之前设置的属性。 命令对象属性设置始终传递到基础数据提供程序而不考虑光标所在的位置。 因此，您可以使用命令对象在任何时间设置的属性。

> [!NOTE]
>  动态属性 DBPROP_SERVERDATAONINSERT 不受游标服务，即使基础数据提供程序支持。

|属性名称|Description|
|-------------------|-----------------|
|自动重新计算 (DBPROP_ADC_AUTORECALC)|此值指示通常如何使用 Data Shaping 服务创建的记录集的计算和聚合列进行计算。 默认值 (值 = 1) 是 Data Shaping 服务确定这些值已发生更改时重新计算。 如果值为 0，最初构建层次结构时，将仅计算的计算或聚合的列。|
|批大小 (DBPROP_ADC_BATCHSIZE)|指示可以在发送到数据存储区之前进行批处理的 update 语句数。 在批处理中的多个语句，往返次数较少的数据存储。|
|缓存子行 (DBPROP_ADC_CACHECHILDROWS)|对于使用 Data Shaping 服务创建的记录集，此值指示是否将子记录集存储在缓存中供以后使用。|
|游标引擎版本 (DBPROP_ADC_CEVER)|指示正在使用的游标服务的版本。|
|维护更改状态 (DBPROP_ADC_MAINTAINCHANGESTATUS)|指示用于重新同步多个表联接中的一个或多个行的命令的文本。|
|[优化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|指示是否应创建索引。 如果设置为 **，则返回 True**，表示允许临时创建索引以提高执行某些操作。|
|[重新调整形状名称](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|指示的名称**记录集**。 可以在当前，引用或后续，数据整理命令。|
|[重新同步命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|指示自定义命令字符串，它由[重新同步](../../../ado/reference/ado-api/resync-method.md)方法时[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)属性是否生效。|
|[唯一目录](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|指示包含在引用的表的数据库的名称**唯一表**属性。|
|[唯一的架构](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|指示中引用的表的所有者的名称**唯一表**属性。|
|[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|指示中的一个表的名称**记录集**创建从多个可以通过插入、 更新或删除操作修改的表。|
|更新条件 (DBPROP_ADC_UPDATECRITERIA)|指示中的哪些字段**其中**子句用于处理在更新期间发生的冲突。|
|[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)(DBPROP_ADC_UPDATERESYNC)|指示是否**重新同步**方法隐式调用之后[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法 （以及其行为），当**唯一表**属性是否生效。|

 此外可以设置或通过指定其名称为索引来检索动态属性**属性**集合。 例如，获取并打印的当前值[优化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)动态属性，然后设置新值，如下所示：

```
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>内置属性行为
 用于 OLE DB 游标服务还会影响某些内置属性的行为。

|属性名称|Description|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|对类型的游标可用于进行了补充**记录集**。|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|对可用于锁的类型进行了补充**记录集**。 启用批处理更新。|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|指定一个或多个字段的名称，**记录集**进行排序，并且是否按升序或降序顺序排序的每个字段。|

## <a name="method-behavior"></a>方法行为
 用于 OLE DB 游标服务启用或影响的行为[字段](../../../ado/reference/ado-api/field-object.md)对象的[追加](../../../ado/reference/ado-api/append-method-ado.md)方法; 并**记录集**对象的[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)，[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，并[保存](../../../ado/reference/ado-api/save-method.md)方法。
