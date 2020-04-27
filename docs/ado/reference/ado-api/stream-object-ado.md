---
title: Stream 对象（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c70a22a3048c769aac343d51e621e4d755d3baeb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67916723"
---
# <a name="stream-object-ado"></a>流对象 (ADO)
表示二进制数据或文本的流。  
  
 在树状层次结构（例如文件系统或电子邮件系统）中，[记录](../../../ado/reference/ado-api/record-object-ado.md)可能具有与之关联的默认二进制位流，其中包含文件或电子邮件的内容。 **流**对象可用于操作包含这些数据流的字段或记录。 可以通过以下方式获取**流**对象：  
  
-   从指向包含二进制或文本数据的对象（通常是文件）的 URL。 此对象可以是一个简单的文档，也可以是一个表示结构化文档的**记录**对象，也可以是一个文件夹。  
  
-   打开与**Record**对象关联的默认**流**对象。 您可以在打开**记录**时获取与**record**对象关联的默认流，以消除仅用于打开流的往返过程。  
  
-   通过实例化一个**流**对象。 这些**流**对象可用于存储用于应用程序的数据。 不同于与 URL 关联的**流**或**记录**的默认**流**，默认情况下，实例化的**流**不与基础源关联。  
  
 使用**流**对象的方法和属性，可以执行以下操作：  
  
-   使用[open](../../../ado/reference/ado-api/open-method-ado-stream.md)方法打开**记录**或 URL 中的**流**对象。  
  
-   使用[close](../../../ado/reference/ado-api/close-method-ado.md)方法关闭**流**。  
  
-   使用[Write](../../../ado/reference/ado-api/write-method.md)和[WriteText](../../../ado/reference/ado-api/writetext-method.md)方法将字节或文本输入到**流**中。  
  
-   用[read](../../../ado/reference/ado-api/read-method.md)和[ReadText](../../../ado/reference/ado-api/readtext-method.md)方法从**流**中读取字节。  
  
-   用[Flush](../../../ado/reference/ado-api/flush-method-ado.md)方法将仍在 ADO 缓冲区中的任何**流**数据写入基础对象。  
  
-   使用[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)方法将**流**的内容复制到另一**流**。  
  
-   通过[SkipLine](../../../ado/reference/ado-api/skipline-method.md)方法和[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)属性控制如何从源文件读取行。  
  
-   用[EOS](../../../ado/reference/ado-api/eos-property.md)属性和[SetEOS](../../../ado/reference/ado-api/seteos-method.md)方法确定流位置的结尾。  
  
-   用[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)和[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)方法保存和还原文件中的数据。  
  
-   指定用于存储包含[字符集](../../../ado/reference/ado-api/charset-property-ado.md)属性的**流**的字符集。  
  
-   使用[Cancel](../../../ado/reference/ado-api/cancel-method-ado.md)方法暂停异步**流**操作。  
  
-   确定具有[Size](../../../ado/reference/ado-api/size-property-ado-stream.md)属性的**流**中的字节数。  
  
-   使用[position](../../../ado/reference/ado-api/position-property-ado.md)属性控制**流**中的当前位置。  
  
-   使用[type](../../../ado/reference/ado-api/type-property-ado-stream.md)属性确定**流**中的数据类型。  
  
-   确定**流**的当前状态（"已关闭"、"打开" 或 "正在执行"）和 "[状态](../../../ado/reference/ado-api/state-property-ado.md)" 属性。  
  
-   使用[mode](../../../ado/reference/ado-api/mode-property-ado.md)属性指定**流**的访问模式。  
  
> [!NOTE]
>  使用 http 方案的 Url 将自动调用[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 **流式**处理对象是安全的。  
  
 本部分包含以下主题。  
  
-   [流对象属性、方法和事件](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [记录和流](../../../ado/guide/data/records-and-streams.md)
