---
title: "Open 方法 （ADO 流） |Microsoft 文档"
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
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dba50c39ff8c31154e52f8575a93acdf829df442
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="open-method-ado-stream"></a>Open 方法 （ADO 流）
打开[流](../../../ado/reference/ado-api/stream-object-ado.md)对象操作的二进制或文本数据的流。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据源*  
 可选。 A **Variant**值，该值指定的数据源**流**。 *源*可能包含指向的已知树状结构，例如电子邮件或文件系统中的现有节点的绝对 URL 字符串。 应使用 URL 关键字指定 URL ("URL =*方案*://*服务器*/*文件夹*")。 或者，*源*可能包含对已打开的引用[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，这将打开与关联的默认流**记录**。 如果*源*未指定，**流**是实例化并打开，默认情况下与任何基础源关联。 有关 URL 方案和其关联的提供程序的详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 *模式*  
 可选。 A [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值，该值指定所产生的访问模式**流**(例如，读/写或只读)。 默认值是**adModeUnknown**。 请参阅[模式](../../../ado/reference/ado-api/mode-property-ado.md)属性以获取有关访问模式的详细信息。 如果*模式*未指定，则它由源对象中继承。 例如，如果源**记录**在只读模式下，打开**流**还将打开默认情况下在只读模式下。  
  
 *OpenOptions*  
 可选。 A [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)值。 默认值是**adOpenStreamUnspecified**。  
  
 *UserName*  
 可选。 A**字符串**值，该值包含的用户标识，如果需要将访问**流**对象。  
  
 *密码*  
 可选。 A**字符串**值，该值包含的密码，如果需要将访问**流**对象。  
  
## <a name="remarks"></a>注释  
 当**记录**作为源参数传入的对象*UserID*和*密码*参数不会使用因为访问**记录**对象已可用。 同样，[模式](../../../ado/reference/ado-api/mode-property-ado.md)的**记录**对象传输到**流**对象。 当*源*未指定，**流**打开不包含任何数据，但[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)为零 (0)。 若要避免丢失任何数据写入到这**流**时**流**是关闭，保存**流**与[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)或[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)方法，或将其保存到另一个内存位置。  
  
 *OpenOptions*值**adOpenStreamFromRecord**标识的内容*源*参数需要已打开**记录**对象。 默认行为是将*源*作为直接指向树状结构，如文件中的节点的 URL。 打开与该节点关联的默认流。  
  
 虽然**流**是未打开，可读取的所有只读属性**流**。 如果**流**异步打开的所有后续操作 (而不检查[状态](../../../ado/reference/ado-api/state-property-ado.md)和其他只读属性) 被阻止，直到**打开**已完成操作。  
  
 除了已前面所述，通过不指定的选项外*源*，你可以创建的实例**流**而无需将它与基础源相关联的内存中的对象。 你可以动态添加数据到流写入到的二进制或文本数据**流**与[编写](../../../ado/reference/ado-api/write-method.md)或[WriteText](../../../ado/reference/ado-api/writetext-method.md)，也可以是从文件加载数据[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Open 方法 （ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)   
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
