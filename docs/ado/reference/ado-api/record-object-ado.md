---
title: Record 对象（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5ffc515350bfff4307da382c05aae50ed1930802
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917363"
---
# <a name="record-object-ado"></a>记录对象 (ADO)
表示[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)或数据提供程序中的行，或由半结构化数据访问接口（如文件或目录）返回的对象。  
  
## <a name="remarks"></a>备注  
 **Record**对象表示一行数据，并与一行**记录集**有一些概念上的相似之处。 根据提供程序的功能，可以直接从提供程序（而不是单行**记录集**）返回**记录**对象，例如，当执行仅选择一行的 SQL 查询时。 或者，可以直接从**记录集**对象获取**记录**对象。 或者，**记录**可以直接从提供程序返回到半结构化数据，例如 Microsoft Exchange OLE DB 提供程序。  
  
 您可以通过**record**对象上的[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合来查看与**record**对象相关联的字段。 ADO 允许对象值列，包括**记录**对象的**Fields**集合中的**记录集**、 **SafeArray**和标量值。  
  
 如果**Record**对象表示**记录集中**的某行，则可以使用[Source](../../../ado/reference/ado-api/source-property-ado-record.md)属性返回到该原始**记录集**。  
  
 **记录**对象还可以由半结构化数据提供程序使用，例如用于[Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)，以及为树状结构命名空间建模。 树中的每个节点都是具有关联列的**记录**对象。 列可以表示该节点的属性和其他相关信息。 **Record**对象可以表示叶节点和树结构中的非叶节点。 非叶节点具有其他节点作为其内容，但叶节点没有此类内容。 叶节点通常包含数据的二进制流，而非叶节点还可能具有与其关联的默认二进制流。 **记录**对象的属性标识节点的类型。  
  
 **Record**对象还表示用于导航分层组织的数据的另一种方法。 可以创建**记录**对象来表示大型树结构中特定子树的根，并可以打开新的**记录**对象来表示子节点。  
  
 可以使用绝对 URL 来唯一标识资源（例如文件或目录）。 当使用绝对 URL 打开**记录**时，将隐式创建[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象并将其设置为**record**对象。 可以通过[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性将**连接**对象显式设置为**Record**对象。 使用**连接**对象可以访问的文件和目录定义了**记录**操作可能发生的*上下文*。  
  
 **记录**对象上的数据修改和导航方法还接受一个相对 url，该 url 将使用绝对 Url 或**连接**对象上下文作为起始点查找资源。  
  
> [!NOTE]
>  使用 http 方案的 Url 将自动调用[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 **连接**对象与每个**Record**对象相关联。 因此，**记录**对象操作可以通过调用**连接**对象事务方法来成为事务的一部分。  
  
 **Record**对象不支持 ADO 事件，因此将不会响应通知。  
  
 对于**Record**对象的方法和属性，您可以执行以下操作：  
  
-   设置或返回具有[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性的关联**连接**对象。  
  
-   使用[Mode](../../../ado/reference/ado-api/mode-property-ado.md)属性指示访问权限。  
  
-   返回目录的 URL （如果有），其中包含具有[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)属性的**记录**所表示的资源。  
  
-   指示用[Source](../../../ado/reference/ado-api/source-property-ado-record.md)属性派生**记录**的绝对 url、相对 url 或**记录集**。  
  
-   用[State](../../../ado/reference/ado-api/state-property-ado.md)属性指示**记录**的当前状态。  
  
-   通过[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)属性指示**记录** - 的*简单*、*集合*或*结构化文档*的类型。  
  
-   使用[Cancel](../../../ado/reference/ado-api/cancel-method-ado.md)方法停止执行异步操作。  
  
-   使用[Close](../../../ado/reference/ado-api/close-method-ado.md)方法将**记录**与数据源解除关联。  
  
-   使用[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)方法将**记录**表示的文件或目录复制到另一个位置。  
  
-   删除使用[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)方法由 a**记录**表示的文件或目录和子目录。  
  
-   使用[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)方法打开一个**记录集**，其中包含的行表示由**记录**表示的实体的子目录和文件。  
  
-   使用[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)方法将**记录**表示的文件（或目录和子目录）移到另一个位置。  
  
-   将**记录**与现有数据源关联，或使用[Open](../../../ado/reference/ado-api/open-method-ado-record.md)方法创建新的文件或目录。  
  
 **记录**对象对于脚本是安全的。  
  
 本部分包含以下主题。  
  
-   [记录对象属性、方法和事件](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [Fields 集合（ADO）](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [记录和流](../../../ado/guide/data/records-and-streams.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
