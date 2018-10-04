---
title: Open 方法 (ADO Stream) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0df165514a10bc667c8bd2cc6d2a8569faa79d11
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611415"
---
# <a name="open-method-ado-stream"></a>Open 方法（ADO 流）
此时将打开[Stream](../../../ado/reference/ado-api/stream-object-ado.md)要操作的二进制或文本数据的流对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据源*  
 可选。 一个**Variant**值，该值指定的数据源**Stream**。 *源*可能包含指向已知的树结构，如电子邮件或文件系统中的现有节点的绝对 URL 字符串。 应通过使用 URL 关键字指定 URL ("URL =*方案*://*服务器*/*文件夹*")。 或者，*源*可能包含对已打开的引用[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，这将打开与关联的默认流**记录**。 如果*源*未指定，则**Stream**是实例化并打开，默认情况下与任何基础源相关联。 有关 URL 方案和其关联的提供程序的详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 *模式*  
 可选。 一个[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值，该值指定所产生的访问模式**Stream** (例如，读/写或只读)。 默认值是**adModeUnknown**。 请参阅[模式下](../../../ado/reference/ado-api/mode-property-ado.md)属性以获取有关访问模式的详细信息。 如果*模式下*未指定，则它由源对象继承。 例如，如果源**记录**在只读模式下打开**Stream**还将打开默认情况下在只读模式下。  
  
 *OpenOptions*  
 可选。 一个[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)值。 默认值是**adOpenStreamUnspecified**。  
  
 *UserName*  
 可选。 一个**字符串**值，该值包含用户标识，如果需要请访问**Stream**对象。  
  
 *密码*  
 可选。 一个**字符串**值，该值包含密码，如果需要请访问**Stream**对象。  
  
## <a name="remarks"></a>备注  
 时**记录**对象作为源参数中传递*UserID*并*密码*参数不能因为访问**记录**对象已可用。 同样，[模式下](../../../ado/reference/ado-api/mode-property-ado.md)的**记录**对象传输到**Stream**对象。 当*源*未指定，则**Stream**打开不包含任何数据，但[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)零 (0)。 若要避免丢失任何数据写入到这**Stream**时**Stream**是已关闭，保存**Stream**与[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)或[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)方法，或将其保存到另一个内存位置。  
  
 *OpenOptions*的值**adOpenStreamFromRecord**标识的内容*源*参数来在已打开**记录**对象。 默认行为是将视为*源*作为 URL 直接指向树状结构，如文件中的节点。 打开与该节点关联的默认流。  
  
 虽然**Stream**是未打开，就可以读取的所有只读属性**Stream**。 如果**Stream**异步打开的所有后续操作 (而不检查[状态](../../../ado/reference/ado-api/state-property-ado.md)和其他只读属性) 被阻止，直到**打开**完成操作。  
  
 除了了前面所述，通过不指定的选项外*源*，可以创建的实例**Stream**而无需将它与基础数据源相关联的内存中对象。 您可以动态地将数据添加到流通过二进制或文本数据写入**Stream**与[编写](../../../ado/reference/ado-api/write-method.md)或[WriteText](../../../ado/reference/ado-api/writetext-method.md)，或通过从文件加载数据[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Open 方法 （ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)   
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
