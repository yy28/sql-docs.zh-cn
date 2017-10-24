---
title: "用于 OLE DB （ADO 服务组件） 的 Microsoft 游标服务 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d7a1f8568b633417196c6c9dda3e8a3615146603
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>OLE DB 概述的 Microsoft 光标服务
OLE DB Microsoft 游标服务将补充数据提供程序的光标支持函数。 因此，用户可以体验相对统一的功能，从所有数据提供程序。

 游标服务提供动态属性，并增强的某些方法的行为。 例如，[优化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)动态属性允许创建临时索引，以便于某些操作，如[查找](../../../ado/reference/ado-api/find-method-ado.md)方法。

 游标服务能够在所有情况下更新批处理的支持。 它还可以模拟功能更强大的游标类型，如动态游标时数据提供程序可以仅提供能力较小的游标，如静态游标。

## <a name="keyword"></a>关键字
 若要调用此服务组件，设置[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)或[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性**adUseClient**。

```
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>动态属性
 OLE DB 游标服务调用时，将下面的动态属性添加到**记录集**对象的[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。 完整列表**连接**和**记录集**中列出对象的动态属性[ADO 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)。 关联的 OLE DB 属性名称，在适当的情况包括在括号中后 ADO 属性名称。

 调用游标服务后，对某些动态属性的更改不可见到基础数据源。 例如，设置*命令超时*属性**记录集**看不见到基础数据提供程序。

```

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 如果你的应用程序需要游标服务，但你需要的基础提供程序上设置动态属性，请调用光标服务之前设置的属性。 命令对象属性设置将始终传递到基础数据提供程序而不考虑光标位置。 因此，你还可以使用命令对象在任何时间设置的属性。

> [!NOTE]
>  动态属性 DBPROP_SERVERDATAONINSERT 不受游标服务，即使基础数据提供程序支持它。

|属性名称|Description|
|-------------------|-----------------|
|自动重新计算 (DBPROP_ADC_AUTORECALC)|为此值指示频率使用数据调整服务创建的记录集计算计算和聚合列。 默认值 (值 = 1) 是每当数据调整服务确定值已更改时重新计算。 如果值为 0，在最初生成层次结构时仅计算的计算或聚合的列。|
|批大小 (DBPROP_ADC_BATCHSIZE)|指示可成批发送到数据存储区之前的 update 语句的数目。 在批处理中的多个语句，往返次数较少的数据存储。|
|缓存子行 (DBPROP_ADC_CACHECHILDROWS)|对于使用数据调整服务创建的记录集，此值指示是否将子记录集存储在缓存中以供将来使用。|
|光标引擎版本 (DBPROP_ADC_CEVER)|指示正在使用的游标服务的版本。|
|维护更改状态 (DBPROP_ADC_MAINTAINCHANGESTATUS)|指示用于重新同步多个表联接中的一个或多个行的命令的文本。|
|[优化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|指示是否应创建索引。 当设置为**True**，授权创建临时索引以提高执行某些操作。|
|[重新调整形状名称](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|指示的名称**记录集**。 可以在当前，引用或后续，调整命令的数据。|
|[重新同步命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|指示使用的自定义命令字符串[重新同步](../../../ado/reference/ado-api/resync-method.md)方法时[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)实际上是属性。|
|[唯一的目录](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|指示包含中引用的表的数据库名称**唯一表**属性。|
|[唯一的架构](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|指示中引用的表的所有者的名称**唯一表**属性。|
|[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|指示中的一个表的名称**记录集**创建从多个可通过插入、 更新或删除操作修改的表。|
|更新条件 (DBPROP_ADC_UPDATECRITERIA)|指示中的哪些字段**其中**子句用于处理更新期间发生的冲突。|
|[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)(DBPROP_ADC_UPDATERESYNC)|指示是否**重新同步**方法隐式调用后[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法 （和其行为），当**唯一表**实际上是属性。|

 你还可以设置或通过指定其名称作为到索引中检索的动态属性**属性**集合。 例如，获取，打印的当前值[优化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)动态属性，然后设置新值，如下所示：

```
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>内置属性行为
 OLE DB 游标服务还会影响某些内置属性的行为。

|属性名称|Description|
|-------------------|-----------------|
|[游标类型](../../../ado/reference/ado-api/cursortype-property-ado.md)|进行补充的类型的游标可用于**记录集**。|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|补充的锁可用于类型**记录集**。 启用批处理更新。|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|指定一个或多个字段的名称，**记录集**进行排序，并且是否按升序或降序排序的每个字段。|

## <a name="method-behavior"></a>方法行为
 OLE DB 游标服务启用或会影响的行为[字段](../../../ado/reference/ado-api/field-object.md)对象的[追加](../../../ado/reference/ado-api/append-method-ado.md)方法; 与**记录集**对象的[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)，[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，和[保存](../../../ado/reference/ado-api/save-method.md)方法。

