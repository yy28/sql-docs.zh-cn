---
title: "记录对象 (ADO) |Microsoft 文档"
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
f1_keywords: Record
helpviewer_keywords: Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0efb504844ac58e7889cdb768821efe95f52e0b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="record-object-ado"></a>记录对象 (ADO)
表示从行[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)或数据提供程序或返回由半结构化的数据提供程序，如文件或目录的对象。  
  
## <a name="remarks"></a>注释  
 A**记录**对象表示一行数据，并具有一个行与一些概念相似之处**记录集**。 根据你提供程序，功能**记录**可能直接从你的提供商，而不是一个行返回对象**记录集**，例如在 SQL 查询选择只有一个行时为执行。 或者，**记录**对象可以直接从获取**记录集**对象。 或者，**记录**于半结构化数据，如 Microsoft Exchange OLE DB 提供程序可以直接从提供程序中返回。  
  
 你可以查看与关联的字段**记录**对象通过[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合**记录**对象。 ADO 允许对象值的列，包括**记录集**， **SafeArray**，和中的标量值**字段**集合**记录**对象。  
  
 如果**记录**对象表示中的行**记录集**，可以返回到该原始**记录集**与[源](../../../ado/reference/ado-api/source-property-ado-record.md)属性。  
  
 **记录**对象还可由半结构化的数据提供程序如[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)、 模型结构树的命名空间。 在树中每个节点都**记录**对象相关联的列。 列可以表示该节点和其他相关信息的属性。 **记录**对象可以表示的叶节点和树状结构中的非叶节点。 非叶节点包含其他节点作为其内容，但叶节点不具有此类内容。 叶节点通常包含二进制流的数据和非叶节点还可能具有与之关联的默认二进制流。 上的属性**记录**对象标识节点的类型。  
  
 **记录**对象还表示一种替代方式导航以分层方式组织数据。 A**记录**对象可能创建来表示一个大型的树状结构中的特定子树的根和新**记录**可能打开对象来表示子节点。  
  
 资源 （例如，文件或目录） 可以唯一标识的绝对 URL。 A[连接](../../../ado/reference/ado-api/connection-object-ado.md)隐式创建对象并将设置为**记录**对象时**记录**打开使用绝对 URL。 A**连接**对象可能显式设置为**记录**对象通过[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性。 文件和目录，可以通过使用访问**连接**对象定义*上下文*顺序**记录**操作可能会出现。  
  
 数据修改和导航方法对**记录**对象还接受定位使用绝对 URL 资源的相对 URL 或**连接**作为起始点的对象上下文。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 A**连接**对象都与每个关联**记录**对象。 因此，**记录**对象操作可以是事务的一部分，通过调用**连接**对象事务方法。  
  
 **记录**对象不支持 ADO 事件，并因此将不响应通知。  
  
 使用方法和属性的**记录**对象，你可以执行以下操作：  
  
-   设置或返回关联**连接**对象[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性。  
  
-   指示使用的访问权限[模式](../../../ado/reference/ado-api/mode-property-ado.md)属性。  
  
-   如果有包含表示的资源返回目录中，URL**记录**与[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)属性。  
  
-   指示绝对 URL、 相对 URL，或**记录集**从中**记录**与派生[源](../../../ado/reference/ado-api/source-property-ado-record.md)属性。  
  
-   指示的当前状态**记录**与[状态](../../../ado/reference/ado-api/state-property-ado.md)属性。  
  
-   指示的一种**记录**-*简单*，*集合*，或*结构化的文档*-与[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)属性。  
  
-   停止与异步操作的执行[取消](../../../ado/reference/ado-api/cancel-method-ado.md)方法。  
  
-   取消关联**记录**与数据源的[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   复制文件或目录由表示**记录**具有另一个位置[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)方法。  
  
-   删除文件或目录和子目录，由表示**记录**与[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)方法。  
  
-   打开**记录集**，其中包含表示子目录和文件所表示的实体的行**记录**与[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)方法。  
  
-   移动 （重命名） 文件，或目录及其子目录，由表示**记录**具有另一个位置[移动记录](../../../ado/reference/ado-api/moverecord-method-ado.md)方法。  
  
-   将关联**记录**与现有的数据源，或创建新文件或目录与[打开](../../../ado/reference/ado-api/open-method-ado-record.md)方法。  
  
 **记录**对象是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [记录对象属性、方法和事件](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [记录和流](../../../ado/guide/data/records-and-streams.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
