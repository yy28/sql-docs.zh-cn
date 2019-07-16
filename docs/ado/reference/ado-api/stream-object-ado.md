---
title: Stream 对象 (ADO) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916723"
---
# <a name="stream-object-ado"></a>流对象 (ADO)
表示二进制数据或文本的流。  
  
 在树状层次结构中的文件系统或电子邮件系统，如[记录](../../../ado/reference/ado-api/record-object-ado.md)可能具有包含该文件或电子邮件的内容与之关联的位的默认二进制流。 一个**Stream**对象可用于操作的字段或包含这些流数据的记录。 一个**Stream**对象可以获取以下方式：  
  
-   从指向包含二进制或文本数据的对象 （通常为文件） 的 URL。 此对象可以是一个简单的文档**记录**对象，表示结构化的文档或一个文件夹。  
  
-   通过打开默认**Stream**与关联的对象**记录**对象。 你可以获取与关联的默认流**记录**对象时**记录**打开时，若要消除只是为了打开流的一个往返。  
  
-   通过实例化**Stream**对象。 这些**Stream**对象可用于将数据存储的应用程序的目的。 与不同**Stream**与 URL 或默认值相关联**Stream**的**记录**，实例化**Stream**与没有关联默认情况下的基础源。  
  
 使用的方法和属性**Stream**对象，您可以执行以下操作：  
  
-   打开**Stream**对象从**记录**或使用 URL[打开](../../../ado/reference/ado-api/open-method-ado-stream.md)方法。  
  
-   关闭**Stream**与[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   输入字节或文本**Stream**与[编写](../../../ado/reference/ado-api/write-method.md)并[WriteText](../../../ado/reference/ado-api/writetext-method.md)方法。  
  
-   读取的字节数从**Stream**与[读取](../../../ado/reference/ado-api/read-method.md)并[ReadText](../../../ado/reference/ado-api/readtext-method.md)方法。  
  
-   编写任何**Stream**仍在 ADO 中的数据缓冲区使用的基础对象[刷新](../../../ado/reference/ado-api/flush-method-ado.md)方法。  
  
-   将复制的内容**Stream**到另一个**Stream**与[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)方法。  
  
-   控制如何从源文件读取行的[SkipLine](../../../ado/reference/ado-api/skipline-method.md)方法并[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)属性。  
  
-   确定流位置与末尾[EOS](../../../ado/reference/ado-api/eos-property.md)属性和[SetEOS](../../../ado/reference/ado-api/seteos-method.md)方法。  
  
-   保存和还原的文件中的数据[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)并[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)方法。  
  
-   指定用于存储使用的字符集**Stream**与[字符集](../../../ado/reference/ado-api/charset-property-ado.md)属性。  
  
-   停止异步**Stream**操作[取消](../../../ado/reference/ado-api/cancel-method-ado.md)方法。  
  
-   确定中的字节数**Stream**与[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)属性。  
  
-   控件中的当前位置**Stream**与[位置](../../../ado/reference/ado-api/position-property-ado.md)属性。  
  
-   确定中的数据类型**Stream**与[类型](../../../ado/reference/ado-api/type-property-ado-stream.md)属性。  
  
-   确定当前的状态**Stream** （关闭、 打开，或执行） 与[状态](../../../ado/reference/ado-api/state-property-ado.md)属性。  
  
-   指定的访问模式**Stream**与[模式](../../../ado/reference/ado-api/mode-property-ado.md)属性。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 **Stream**对象是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [Stream 对象属性、 方法和事件](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [记录和流](../../../ado/guide/data/records-and-streams.md)
