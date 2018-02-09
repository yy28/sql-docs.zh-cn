---
title: "记录和提供程序提供的字段 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5341eac5d18d222e2e0d1f97a006179ffa8927d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="records-and-provider-supplied-fields"></a>记录和提供程序提供的字段
当[记录](../../../ado/reference/ado-api/record-object-ado.md)打开对象，其源可以是已打开的当前行[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，绝对 URL 或相对 URL 结合打开[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象.  
  
 如果**记录**从打开**记录集**、**记录**对象[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合将包含中的所有字段**记录集**，以及由基础提供程序添加任何字段。  
  
 提供程序可能会插入其他字段作为补充特征**记录**。 因此，**记录**可能未显示在具有唯一字段**记录集**作为一个整体或任何**记录**派生自的另一行**记录集**.  
  
 例如，所有行的**记录集**派生自数据源可能对等列作为从，以及使用者电子邮件。 A**记录**派生自的**记录集**将具有不同的字段。 但是，**记录**还可能具有唯一的特定的消息所表示的其他字段**记录**，如附件和抄送 （副本）。  
  
 尽管**记录**对象和当前行的**记录集**具有不同的字段，它们仍然是不同因为**记录**和**记录集**对象具有不同的方法和属性。  
  
 字段由共同持有**记录**和**记录集**可以在可能是对象上修改。 但是，该字段不能删除上**记录**对象，尽管基础提供程序可能支持将字段设置为 null。  
  
 后**记录**是打开，你可以以编程方式添加字段。 你还可以删除已添加的字段，但不是能删除字段与原始**记录集**。  
  
 你也可以打开**记录**直接从 URL 的对象。 在这种情况下，字段添加到**记录**依赖于基础提供程序。 目前，大多数提供程序添加描述所表示的实体的字段的一组**记录**。 如果实体包含的字节，如简单文件流[流](../../../ado/reference/ado-api/stream-object-ado.md)通常可从中打开对象**记录**。  
  
## <a name="special-fields-for-document-source-providers"></a>文档的特殊字段源提供程序  
 一类特殊的提供程序，称为*文档源提供程序*、 管理文件夹和文档。 当**记录**对象表示文档或**记录集**对象表示文档的文件夹、 文档源提供程序填充这些对象包含一组独特的描述字段文档的特征相反的实际文档本身。 通常，一个字段包含对引用**流**表示的文档。  
  
 这些字段构成资源**记录**或**记录集**和为特定的提供程序支持在列出[附录 a： 提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)。  
  
 两个常量索引**字段**的资源集合**记录**或**记录集**检索的成对的常用的字段。 **字段**对象[值](../../../ado/reference/ado-api/value-property-ado.md)属性返回所需的内容。  
  
-   通过访问的字段**adDefaultStream**常量包含与相关联的默认流**记录**或**记录集**对象。 提供程序将默认流分配给对象。  
  
-   通过访问的字段**adRecordURL**常量包含标识文档的绝对 URL。  
  
 文档源提供程序不支持[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合**记录**和**字段**对象。 内容**属性**集合是此类对象为 null。  
  
 文档源提供程序可能添加提供程序特定属性如**数据源类型**以确定它是否文档源提供程序。 有关如何确定你的提供程序的类型的详细信息，请参阅提供程序文档。  
  
## <a name="resource-recordset-columns"></a>资源记录集列  
 A*资源记录集*包含以下各列。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|只读。 指示资源的 URL。|  
|RESOURCE_PARENTNAME|AdVarWChar|只读。 指示父记录的绝对 URL。|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|只读。 指示该资源，即 PARENTNAME 和 PARSENAME 的串联的绝对 URL。|  
|RESOURCE_ISHIDDEN|adBoolean|如果资源处于隐藏状态，则为 true。 除非显式创建行集的命令选择其中 RESOURCE_ISHIDDEN 为 True 的行，将不返回任何行。|  
|RESOURCE_ISREADONLY|adBoolean|如果资源是只读的则为 true。 尝试打开此资源具有 DBBINDFLAG_WRITE 和将失败，并 DB_E_READONLY。 可以编辑此属性，即使只能以只读打开资源。|  
|RESOURCE_CONTENTTYPE|AdVarWChar|指示可能使用文档 — 例如，某个律师的简短。 这可能对应于用于创建文档的 Office 模板。|  
|RESOURCE_CONTENTCLASS|AdVarWChar|指示文档中，如指示格式的 MIME 类型"`text/html`"。|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|指示在其中存储内容的语言。|  
|RESOURCE_CREATIONTIME|adFileTime|只读。 指示包含资源的创建的时间的 FILETIME 结构。 该时间采用协调世界时 (UTC) 格式报告。|  
|RESOURCE_LASTACCESSTIME|AdFileTime|只读。 指示包含上次访问资源的时间的 FILETIME 结构。 时间是 UTC 格式。 FILETIME 成员均为零，如果提供程序不支持此时间成员。|  
|RESOURCE_LASTWRITETIME|AdFileTime|只读。 指示包含资源上次写入时间 FILETIME 结构。 时间是 UTC 格式。 FILETIME 成员均为零，如果提供程序不支持此时间成员。|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|只读。 指示资源的默认流，以字节为单位的大小。|  
|RESOURCE_ISCOLLECTION|adBoolean|只读。 如果资源是一个集合，例如一个目录，则为 true。 如果资源是一个简单的文件，则为 false。|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|adBoolean|如果资源是结构化的文档，则为 true。 如果资源不是结构化的文档，则为 false。 它可以为集合或一个简单的文件。|  
|DEFAULT_DOCUMENT|AdVarWChar|只读。 指示此资源包含到的文件夹的默认简单文档或结构化的文档的 URL。 从资源请求的默认流时使用。 此属性是一个简单的文件为空。|  
|CHAPTERED_CHILDREN|AdChapter|只读。 選擇性。 指示包含资源的子级的行集的章节。 ( *OLE DB Provider for Internet 发布*不使用此列。)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|只读。 指示该资源的显示名称。|  
|RESOURCE_ISROOT|adBoolean|只读。 如果资源是集合或结构化的文档的根，则为 true。|  
  
## <a name="see-also"></a>另请参阅  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
