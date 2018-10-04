---
title: 记录集对象 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bf2aab4e9f11ff3dae9852dd80007867fe5a462
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770825"
---
# <a name="recordset-object-ado"></a>记录集对象 (ADO)
表示整个记录集的基础表或执行命令的结果中。 任何时候**记录集**对象是指仅为当前记录集内的单个记录。  
  
## <a name="remarks"></a>备注  
 您使用**记录集**对象处理从提供程序的数据。 当使用 ADO 时，操作几乎完全使用数据**记录集**对象。 所有**记录集**对象包含的记录 （行） 和字段 （列）。 根据提供程序，支持的功能一些**记录集**方法或属性可能不可用。  
  
 ADODB。记录集是用于创建 ProgID**记录集**对象。 引用过时的 ADOR 的现有应用程序。记录集 ProgID 将继续工作而无需重新编译，但新的开发应引用 ADODB。记录集。  
  
 有在 ADO 中定义的四种不同的游标类型：  
  
-   **动态游标**允许您查看添加、 更改和删除操作的其他用户; 允许所有类型的通过移动**记录集**，不依赖于书签; 并都允许书签，如果提供程序支持它们。  
  
-   **由键集游标**Behaves 像动态游标，但它不允许您查看记录的其他用户一样添加，并禁止对其他用户删除的记录的访问。 由其他用户的数据更改仍将可见。 它始终支持书签，并因此允许所有类型的通过移动**记录集**。  
  
-   **静态游标**提供了一组记录，以便用于查找数据或生成报告的静态副本; 始终允许书签，从而允许所有类型的通过移动**记录集**。 添加、 更改或删除其他用户将不可见。 这是唯一的游标打开客户端时允许使用类型**记录集**对象。  
  
-   **只进游标**允许您仅向前滚动**记录集**。 添加、 更改或删除其他用户将不可见。 这在需要进行仅经过一次的情况下提高性能**记录集**。  
  
 设置[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)属性，然后打开**记录集**来选择游标类型，或传递*CursorType*自变量与[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法。 某些提供程序不支持所有的游标类型。 检查提供程序的文档。 如果未指定游标类型，ADO 将只进游标打开默认情况下。  
  
 如果[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**以打开**记录集**，则**UnderlyingValue** 属性[字段](../../../ado/reference/ado-api/field-object.md)对象中返回没有**记录集**对象。 当与某些提供程序 （如 OLE DB 结合使用 Microsoft SQL Server 的 Microsoft ODBC 提供程序） 一起使用，您可以创建**记录集**独立于以前定义的对象[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象表示通过连接字符串具有**打开**方法。 仍会 ADO[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，但它不会将该对象分配给对象变量。 但是，如果您正在打开多个**记录集**对象通过相同的连接，应显式创建并打开**连接**对象; 此分配**连接**给对象变量的对象。 如果打开时，不要使用此对象变量你**记录集**对象，创建一个新的 ADO**连接**每个对象新**记录集**，即使传递相同连接字符串。  
  
 您可以创建任意多个**记录集**对象根据需要。  
  
 当打开**记录集**，将当前记录放到第一条记录 （如果有） 和[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)并[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性设置为**False**. 如果没有记录**BOF**并**EOF**属性设置不**True**。  
  
 可以使用[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)， **MoveLast**， **MoveNext**，以及**MovePrevious**方法;[移动](../../../ado/reference/ado-api/move-method-ado.md)方法;并[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)， [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)，并[筛选器](../../../ado/reference/ado-api/filter-property.md)属性重新定位假设的提供程序支持相关的当前记录功能。 只进**记录集**对象的对象仅支持[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。 当你使用**移动**方法来访问每个记录 (或枚举**记录集**)，可以使用**BOF**并**EOF**属性确定是否您已移动到开头或末尾以外**记录集**。  
  
 使用的任何功能之前**记录集**对象，必须调用**支持**若要验证的功能也受支持或不可在对象上的方法。 您必须使用功能时**支持**方法返回 false。 例如，可以使用**MovePrevious**方法仅当`Recordset.Supports(adMovePrevious)`返回**True**。 否则，将收到错误，因为**记录集**对象可能已关闭，并且功能呈现的实例上不可用。 如果不支持你感兴趣的功能，则**支持**也将返回 false。 在这种情况下，应避免在调用相应的属性或方法**记录集**对象。  
  
 **记录集**对象可以支持两种类型的更新： 即时和批处理。 立即更新中对数据的所有更改将立即都写入基础数据源调用[更新](../../../ado/reference/ado-api/update-method.md)方法。 你还可以作为参数传递值的数组[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)并**更新**方法，并同时更新记录中的多个字段。  
  
 如果访问接口支持批量更新，则可以缓存到多个记录的更改，然后将其传输到与数据库的单个调用中的提供程序[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 这适用于所做的更改**AddNew**，**更新**，并[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法。 调用后**UpdateBatch**方法中，可以使用[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性来检查是否任何数据冲突以解决这些问题。  
  
> [!NOTE]
>  若要执行的查询，而无需使用[命令](../../../ado/reference/ado-api/command-object-ado.md)对象，请将传递到查询字符串**打开**方法**记录集**对象。 但是，**命令**对象是必需的当你想要保留的命令文本并重新执行它，或使用查询参数。  
  
 [模式下](../../../ado/reference/ado-api/mode-property-ado.md)属性控制访问权限。  
  
 **字段**集合是的默认成员**记录集**对象。 因此，以下两个代码语句是等效的。  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 当**记录集**跨进程，仅传递对象**行集**值封送，和的属性**记录集**对象将被忽略。 Unmarshalling，期间**行集**解压缩到新创建**记录集**对象，它还将其属性设置为默认值。  
  
 **记录集**对象是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [记录集对象属性、 方法和事件](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
