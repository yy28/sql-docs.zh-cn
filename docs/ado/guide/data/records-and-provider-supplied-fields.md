---
title: 记录和提供程序提供的字段 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c64555e0035de8a06d3bb9227262f4202f73f9a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52538054"
---
# <a name="records-and-provider-supplied-fields"></a>记录和提供程序提供的字段
当[记录](../../../ado/reference/ado-api/record-object-ado.md)打开对象，其源可以是一种开放的当前行[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，绝对 URL 或打开与结合使用的相对 URL[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象.  
  
 如果**记录**从打开**记录集**，则**记录**对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合将包含从的所有字段**记录集**，以及由基础提供程序添加任何字段。  
  
 提供程序可能会插入其他字段作为补充的特征**记录**。 因此，**记录**可能不能在具有唯一字段**记录集**作为一个整体或任何**记录**派生自的另一行**记录集**.  
  
 例如，所有行的**记录集**派生自数据源可能对此类为从，列以及使用者电子邮件。 一个**记录**派生自该**记录集**将具有相同的字段。 但是，**记录**可能还有其他字段与特定消息所表示的唯一**记录**，例如附件和抄送 （副本）。  
  
 尽管**记录**对象和当前行**记录集**具有相同的字段，它们是不同的因为**记录**和**记录集**对象具有不同的方法和属性。  
  
 共同之处的字段**记录**并**记录集**可以在任一对象上修改。 但是，不能删除字段上**记录**对象，尽管基础提供程序可能支持的字段设置为 null。  
  
 之后**记录**是打开，你可以以编程方式添加字段。 此外可以删除已添加的字段，但不是能删除字段，从原始**记录集**。  
  
 此外可以打开**记录**直接从 URL 的对象。 在这种情况下，字段添加到**记录**依赖于基础提供程序。 目前，大多数提供程序添加的一组描述表示的实体的字段**记录**。 如果该实体包含流的字节数，一个简单的文件，如[Stream](../../../ado/reference/ado-api/stream-object-ado.md)通常可以从打开对象**记录**。  
  
## <a name="special-fields-for-document-source-providers"></a>有关文档的特殊字段源代码提供程序  
 一种特殊类的提供程序，称为*记录源提供程序*、 管理文件夹和文档。 当**记录**对象表示一种文档或者**记录集**对象表示文档的文件夹、 文档源提供程序填充这些对象包含一组独特的描述字段特征的文档而是实际的文档本身。 通常情况下，一个字段包含的引用**Stream**表示的文档。  
  
 这些字段构成资源**记录**或**记录集**列出支持这些中的特定提供程序和[附录 a:提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)。  
  
 两个常量索引**字段**的资源集合**记录**或**记录集**检索两个常用的字段。 **字段**对象[值](../../../ado/reference/ado-api/value-property-ado.md)属性返回所需的内容。  
  
-   使用访问的字段**adDefaultStream**常量包含默认流与相关联**记录**或**记录集**对象。 提供程序向对象赋予默认流。  
  
-   使用访问的字段**adRecordURL**常量包含标识文档的绝对 URL。  
  
 文档源提供程序不支持[属性](../../../ado/reference/ado-api/properties-collection-ado.md)系列**记录**并**字段**对象。 内容**属性**集合是此类对象为 null。  
  
 文档源提供程序可能会添加特定于提供程序的属性，例如**数据源类型**来确定它是文档的源提供程序。 有关如何确定您的提供程序类型的详细信息，请参阅提供程序文档。  
  
## <a name="resource-recordset-columns"></a>资源记录集列  
 一个*资源记录集*以下列组成。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|只读。 指示该资源的 URL。|  
|RESOURCE_PARENTNAME|AdVarWChar|只读。 指示父记录的绝对 URL。|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|只读。 指示资源，这是 PARENTNAME 和 PARSENAME 的串联的绝对 URL。|  
|RESOURCE_ISHIDDEN|adBoolean|如果资源处于隐藏状态，则为 true。 除非显式创建行集的命令选择的行，其中 RESOURCE_ISHIDDEN 是 True，则会不返回任何行。|  
|RESOURCE_ISREADONLY|adBoolean|如果资源是只读的则为 true。 尝试打开此资源具有 DBBINDFLAG_WRITE 和将因 DB_E_READONLY 失败。 即使在仅进行读取打开的资源时，可以编辑此属性。|  
|RESOURCE_CONTENTTYPE|AdVarWChar|指示文档最有可能使用-例如，某个律师的简短。 这可能对应于用于创建文档的 Office 模板。|  
|RESOURCE_CONTENTCLASS|AdVarWChar|指示文档，如指示格式的 MIME 类型"`text/html`"。|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|指示在其中存储内容的语言。|  
|RESOURCE_CREATIONTIME|adFileTime|只读。 指示 FILETIME 结构，其中包含该资源的创建的时间。 该时间以协调世界时 (UTC) 格式报告。|  
|RESOURCE_LASTACCESSTIME|AdFileTime|只读。 指示 FILETIME 结构，其中包含上一次访问该资源的时间。 时间采用 UTC 格式。 FILETIME 成员均为零，如果提供程序不支持此时间成员。|  
|RESOURCE_LASTWRITETIME|AdFileTime|只读。 指示 FILETIME 结构，其中包含上次写入资源的时间。 时间采用 UTC 格式。 FILETIME 成员均为零，如果提供程序不支持此时间成员。|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|只读。 指示资源的默认流，以字节为单位的大小。|  
|RESOURCE_ISCOLLECTION|adBoolean|只读。 如果资源是一个集合，例如目录，则为 true。 如果资源是一个简单的文件，则为 false。|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|adBoolean|如果资源是结构化的文档，则为 true。 如果资源不是结构化的文档，则为 false。 它可能是一个集合或一个简单的文件。|  
|DEFAULT_DOCUMENT|AdVarWChar|只读。 指示此资源包含文件夹的默认简单文档或结构化的文档的 URL。 从资源请求的默认流时使用。 此属性是一个简单的文件为空。|  
|CHAPTERED_CHILDREN|adChapter|只读。 可选。 指示包含资源的子级的行集的一章。 ( *OLE DB 访问接口用于 Internet 发布*不使用此列。)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|只读。 指示该资源的显示名称。|  
|RESOURCE_ISROOT|adBoolean|只读。 如果资源是集合或结构化的文档的根，则为 true。|  
  
## <a name="see-also"></a>请参阅  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
