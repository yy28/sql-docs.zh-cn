---
title: 记录对象 (ADO) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 859bf3f53051a500e86742cb681885b8067f6a0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712216"
---
# <a name="record-object-ado"></a>记录对象 (ADO)
表示从行[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)或数据提供程序或返回由半结构化的数据提供程序，如文件或目录的对象。  
  
## <a name="remarks"></a>备注  
 一个**记录**对象表示一行数据，并具有一个行与一些概念相似之处**记录集**。 具体取决于您的提供商的功能**记录**直接从您的提供程序而不是一个行可能会返回对象**记录集**，例如时可以选择只有一个行的 SQL 查询为执行。 或者，**记录**可以直接从获取对象**记录集**对象。 或者，**记录**半结构化数据，如 Microsoft Exchange OLE DB 访问接口可以直接从提供程序中返回。  
  
 您可以查看与关联的字段**记录**对象的[字段](../../../ado/reference/ado-api/fields-collection-ado.md)上的收集**记录**对象。 ADO 允许对象值的列，包括**记录集**， **SafeArray**，和中的标量值**字段**系列**记录**对象。  
  
 如果**记录**对象表示中的一行**记录集**，则可以返回到该原始图像**记录集**与[源](../../../ado/reference/ado-api/source-property-ado-record.md)属性。  
  
 **记录**对象也可由半结构化的数据提供程序如[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)、 建模结构树的命名空间。 在树中每个节点都**记录**对象相关联的列。 列可以表示该节点和其他相关信息的属性。 **记录**对象可以表示叶节点和非叶节点的树状结构中。 非叶节点具有其他节点作为其内容，但是叶节点不具有此类内容。 叶节点通常包含二进制流的数据和非叶节点还可能具有与之关联的默认二进制流。 上的属性**记录**对象标识的节点类型。  
  
 **记录**对象还表示的另一个方法，用于导航层次结构组织数据。 一个**记录**对象可能是创建用于表示大型的树状结构中的特定子树的根和新**记录**可能打开对象来表示子节点。  
  
 绝对 URL 可以唯一标识的资源 （例如，文件或目录）。 一个[连接](../../../ado/reference/ado-api/connection-object-ado.md)隐式创建对象并设置为**记录**对象时**记录**使用绝对 URL 打开。 一个**连接**对象显式设置为**记录**对象通过[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性。 文件和目录，可以通过访问**连接**对象定义*上下文*所在**记录**操作可能会发生。  
  
 上的数据修改和导航方法**记录**对象还接受定位使用绝对 URL 的资源的相对 URL 或**连接**作为起始点的对象上下文。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 一个**连接**对象将与每个相关联**记录**对象。 因此，**记录**对象操作可以通过调用是事务的一部分**连接**对象事务的方法。  
  
 **记录**对象不支持 ADO 事件，因此不会响应的通知。  
  
 使用的方法和属性**记录**对象，您可以执行以下操作：  
  
-   设置或返回关联**连接**对象[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性。  
  
-   指示使用的访问权限[模式下](../../../ado/reference/ado-api/mode-property-ado.md)属性。  
  
-   如果有包含表示的资源返回的目录的 URL**记录**与[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)属性。  
  
-   指示绝对 URL，相对 URL，或**记录集**从中**记录**与派生[源](../../../ado/reference/ado-api/source-property-ado-record.md)属性。  
  
-   指示当前的状态**记录**与[状态](../../../ado/reference/ado-api/state-property-ado.md)属性。  
  
-   指示的类型**记录** - *简单*，*集合*，或*结构化的文档*-使用[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)属性。  
  
-   停止与异步操作的执行[取消](../../../ado/reference/ado-api/cancel-method-ado.md)方法。  
  
-   取消关联**记录**从数据源与[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   复制文件或目录由**记录**到另一个位置与[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)方法。  
  
-   删除文件或目录和子目录，由此**记录**与[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)方法。  
  
-   打开**记录集**，其中包含表示子目录和文件表示的实体的行**记录**与[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)方法。  
  
-   移动 （重命名） 文件或目录和子目录，由此**记录**到另一个位置与[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)方法。  
  
-   将相关联**记录**与现有数据源，或创建新的文件或目录[打开](../../../ado/reference/ado-api/open-method-ado-record.md)方法。  
  
 **记录**对象是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [记录对象属性、方法和事件](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [记录和流](../../../ado/guide/data/records-and-streams.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
