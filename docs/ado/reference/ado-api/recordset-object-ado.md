---
title: "记录集对象 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset
helpviewer_keywords: Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 02d767f733ed8cb3767d49cf092ff67d1e37ef54
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="recordset-object-ado"></a>记录集对象 (ADO)
表示整个组记录从基表或执行命令的结果。 在任何时候，**记录集**对象是指仅为当前记录集内的单个记录。  
  
## <a name="remarks"></a>注释  
 你使用**记录集**对象来操作从提供程序的数据。 使用 ADO 时，操作几乎完全使用数据**记录集**对象。 所有**记录集**对象包含的记录 （行） 和字段 （列）。 根据提供程序，支持的功能某些**记录集**方法或属性可能不可用。  
  
 ADODB。记录集是用于创建的 ProgID**记录集**对象。 引用过时的 ADOR 的现有应用程序。记录集 ProgID 将继续工作无需重新编译，但新的开发应引用 ADODB。记录集。  
  
 有在 ADO 中定义的四种不同的游标类型：  
  
-   **动态游标**，您可以查看添加、 更改和其他用户; 通过删除允许所有类型的通过移动**记录集**，不依赖于书签; 并都允许书签，如果该提供程序支持它们。  
  
-   **键集游标**类似动态游标，但它不允许您查看记录的其他用户的行为方式与添加，并阻止对其他用户删除的记录的访问。 数据更改由其他用户仍将可见。 它始终支持书签，从而使得可以通过移动所有类型**记录集**。  
  
-   **静态游标**提供一组为你要用于查找数据或生成报表的记录的静态副本; 始终允许书签，从而使得可以通过移动所有类型**记录集**。 添加、 更改或删除其他用户将不可见。 这是唯一的游标打开客户端时，允许类型**记录集**对象。  
  
-   **只进游标**可以仅向前滚动**记录集**。 添加、 更改或删除其他用户将不可见。 这提高了在你需要执行一次传递仅的位置的情况下的性能**记录集**。  
  
 设置[游标类型](../../../ado/reference/ado-api/cursortype-property-ado.md)属性，然后打开**记录集**选择游标类型，或传递*游标类型*参数与[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法。 某些提供程序不支持所有游标类型。 请检查提供程序的文档。 如果你没有指定游标类型，ADO 默认情况下打开只进游标。  
  
 如果[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**以打开**记录集**、 **UnderlyingValue** 属性[字段](../../../ado/reference/ado-api/field-object.md)对象不可用在返回**记录集**对象。 当与某些提供程序 （如 Microsoft ODBC OLE DB 提供程序结合使用 Microsoft SQL Server） 一起使用，您可以创建**记录集**独立于以前定义的对象[连接](../../../ado/reference/ado-api/connection-object-ado.md)通过传递使用的连接字符串的对象**打开**方法。 ADO 仍会产生[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，但它不会将该对象分配给对象变量。 但是，如果要打开多个**记录集**对象通过相同的连接，你应显式创建并打开**连接**对象; 此分配**连接**给对象变量的对象。 如果打开时，不要使用此对象变量你**记录集**对象，创建一个新的 ADO**连接**每个对象新**记录集**，即使传递相同连接字符串。  
  
 你可以创建任意多个**记录集**对象根据需要。  
  
 当你打开**记录集**，将当前记录放到第一条记录 （如果有） 和[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)和[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性设置为**False**. 如果不有任何记录， **BOF**和**EOF**属性设置不**True**。  
  
 你可以使用[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)， **MoveLast**， **MoveNext**，和**MovePrevious**方法;[移动](../../../ado/reference/ado-api/move-method-ado.md)方法;与[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)， [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)，和[筛选器](../../../ado/reference/ado-api/filter-property.md)属性重新定位假定该提供程序支持相关的当前记录功能。 只进**记录集**对象仅支持[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。 当你使用**移动**方法访问每个记录 (或枚举**记录集**)，你可以使用**BOF**和**EOF**属性设置为确定是否您已移动到开头或末尾以外**记录集**。  
  
 在使用的任何功能之前**记录集**对象，必须调用**支持**上要验证的功能是支持或不可用的对象的方法。 你必须未使用的功能时**支持**方法返回 false。 例如，你可以使用**MovePrevious**方法才`Recordset.Supports(adMovePrevious)`返回**True**。 否则，将收到错误，因为**记录集**对象可能已关闭，功能呈现的实例上不可用。 如果不支持你感兴趣的功能，则**支持**也将返回 false。 在这种情况下，应避免调用对应的属性或方法**Recrodset**对象。  
  
 **记录集**对象可以支持两种类型的更新： 立即和批处理。 在即时更新中，对数据的所有更改都写入立即到基础数据源一旦调用[更新](../../../ado/reference/ado-api/update-method.md)方法。 你还可以通过以下方式传递值的数组作为参数使用[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)和**更新**方法并同时更新记录中的多个字段。  
  
 如果提供程序支持批处理更新，你可以缓存对多个记录的更改，然后将它们传输到与数据库的单次调用中的提供程序[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 这适用于所做的更改**AddNew**，**更新**，和[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法。 调用后**UpdateBatch**方法，你可以使用[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性可以检查是否任何数据冲突，为了解决这些问题。  
  
> [!NOTE]
>  执行查询，而使用[命令](../../../ado/reference/ado-api/command-object-ado.md)对象，查询将字符串传递给**打开**方法**记录集**对象。 但是，**命令**对象是必需的当你想要保留的命令文本并重新执行它，或使用查询参数。  
  
 [模式](../../../ado/reference/ado-api/mode-property-ado.md)属性控制访问权限。  
  
 **字段**集合是的默认成员**记录集**对象。 因此，下面的两个代码语句是等效的。  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 当**记录集**跨进程，仅传递对象**行集**值封送，和的属性**记录集**对象将被忽略。 期间 unmarshalling，**行集**是解压缩到新创建**记录集**对象，它还将其属性设置为默认值。  
  
 **记录集**对象是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [记录集对象属性、 方法和事件](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
