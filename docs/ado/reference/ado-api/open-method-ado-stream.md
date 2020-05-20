---
title: Open 方法（ADO 流） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d59fcbbd7edea7ac87b2c080d27160cb98732759
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762155"
---
# <a name="open-method-ado-stream"></a>Open 方法（ADO 流）
打开一个[流](../../../ado/reference/ado-api/stream-object-ado.md)对象以处理二进制或文本数据的流。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>参数  
 *源*  
 可选。 一个**变量**值，指定**流**的数据源。 *源*可以包含指向已知树结构（如电子邮件或文件系统）中的现有节点的绝对 URL 字符串。 Url 应使用 url 关键字（"url =*方案*：//*服务器* / *文件夹*"）来指定。 另外， *Source*可能包含对已打开的[record](../../../ado/reference/ado-api/record-object-ado.md)对象的引用，该对象将打开与该**记录**关联的默认流。 如果未指定*源*，则默认情况下，将实例化并打开一个**流**，而不会关联到任何基础源。 有关 URL 方案及其关联的提供程序的详细信息，请参阅[绝对和相对 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 *模式*  
 可选。 一个[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值，该值指定结果**流**的访问模式（例如，读/写或只读）。 默认值为**adModeUnknown**。 有关访问模式的详细信息，请参阅[模式](../../../ado/reference/ado-api/mode-property-ado.md)属性。 如果未指定模式，则源对象将继承该*模式*。 例如，如果以只读模式打开了源**记录**，则默认情况下，将在只读模式下打开**流**。  
  
 *OpenOptions*  
 可选。 [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)值。 默认值为**adOpenStreamUnspecified**。  
  
 *用户名*  
 可选。 一个**字符串**值，该值包含用户标识，如有必要，它将访问**流**对象。  
  
 *密码*  
 可选。 一个**字符串**值，该值包含在需要时访问**流**对象的密码。  
  
## <a name="remarks"></a>备注  
 作为 source 参数传入**记录**对象时，不使用*UserID*和*Password*参数，因为对**记录**对象的访问已可用。 同样，将**记录**对象的[模式](../../../ado/reference/ado-api/mode-property-ado.md)传输到**Stream**对象。 如果未指定*源*，则打开的**流**不包含任何数据，并且[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)为零（0）。 若要避免在**流**关闭时丢失写入到此**流**的任何数据，请用[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)或[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)方法保存该**流**，或将其保存到其他内存位置。  
  
 **AdOpenStreamFromRecord**的*OpenOptions*值将*源*参数的内容标识为已打开的**记录**对象。 默认行为是将*源*视为直接指向树结构（如文件）中的节点的 URL。 将打开与该节点关联的默认流。  
  
 当**流**未打开时，可以读取**流**的所有只读属性。 如果**流**是异步打开的，则所有后续操作（除检查[状态](../../../ado/reference/ado-api/state-property-ado.md)和其他只读属性以外）都将被阻止，直到**打开**操作完成。  
  
 除了前面所述的选项，通过不指定*源*，你可以在内存中创建**流**对象的实例，而无需将其与基础源关联。 可以通过将二进制数据或文本数据写入**到流中**，[或者使用](../../../ado/reference/ado-api/write-method.md) [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)从[文件中加载数据，从而](../../../ado/reference/ado-api/writetext-method.md)将数据动态添加到流中。  
  
## <a name="applies-to"></a>应用于  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Open 方法（ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法（ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)   
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
