---
title: "流对象 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b074a26bdd82bd4356620dbd0b12dc0b7f1c75c7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="stream-object-ado"></a>流对象 (ADO)
表示二进制数据或文本的流。  
  
 在树结构层次结构中的文件系统或电子邮件系统，如[记录](../../../ado/reference/ado-api/record-object-ado.md)可能具有包含文件或电子邮件的内容与之关联的位的默认二进制流。 A**流**对象可以用于操作字段或包含这些数据流的数据的记录。 A**流**可以通过以下方式获取对象：  
  
-   从指向包含二进制或文本数据的对象 （通常为文件） 的 URL。 此对象可以是一个简单的文档，**记录**表示结构化的文档或文件夹对象。  
  
-   通过打开默认**流**与关联的对象**记录**对象。 你可以获取与关联的默认流**记录**对象时**记录**打开时，若要消除一次往返行程，即可打开流。  
  
-   通过实例化**流**对象。 这些**流**对象可以用于你的应用程序用于存储数据。 与不同**流**URL 或默认值与关联**流**的**记录**，实例化**流**与没有关联默认情况下的基础源。  
  
 使用方法和属性的**流**对象，你可以执行以下操作：  
  
-   打开**流**对象**记录**或使用 URL[打开](../../../ado/reference/ado-api/open-method-ado-stream.md)方法。  
  
-   关闭**流**与[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   输入字节或文本**流**与[编写](../../../ado/reference/ado-api/write-method.md)和[WriteText](../../../ado/reference/ado-api/writetext-method.md)方法。  
  
-   读取字节的字节**流**与[读取](../../../ado/reference/ado-api/read-method.md)和[ReadText](../../../ado/reference/ado-api/readtext-method.md)方法。  
  
-   编写任何**流**仍在 ADO 数据缓冲到的基础对象[刷新](../../../ado/reference/ado-api/flush-method-ado.md)方法。  
  
-   内容复制**流**到另一个**流**与[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)方法。  
  
-   控制行从源文件的读取方式[SkipLine](../../../ado/reference/ado-api/skipline-method.md)方法和[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)属性。  
  
-   确定使用的流位置末尾[EOS](../../../ado/reference/ado-api/eos-property.md)属性和[SetEOS](../../../ado/reference/ado-api/seteos-method.md)方法。  
  
-   保存并还原使用的文件中的数据[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)和[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)方法。  
  
-   指定用于存储使用的字符集**流**与[Charset](../../../ado/reference/ado-api/charset-property-ado.md)属性。  
  
-   暂停异步**流**操作[取消](../../../ado/reference/ado-api/cancel-method-ado.md)方法。  
  
-   确定中的字节数**流**与[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)属性。  
  
-   控制中的当前位置**流**与[位置](../../../ado/reference/ado-api/position-property-ado.md)属性。  
  
-   确定中的数据类型**流**与[类型](../../../ado/reference/ado-api/type-property-ado-stream.md)属性。  
  
-   确定的当前状态**流**（关闭时打开，或执行） 与[状态](../../../ado/reference/ado-api/state-property-ado.md)属性。  
  
-   指定的访问模式**流**与[模式](../../../ado/reference/ado-api/mode-property-ado.md)属性。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 **流**对象是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [流对象属性、 方法和事件](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [记录和流](../../../ado/guide/data/records-and-streams.md)
