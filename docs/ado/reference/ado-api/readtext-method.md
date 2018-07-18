---
title: ReadText 方法 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7c3e2dcf695e9c6748881656d87e02404209dbf
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280776"
---
# <a name="readtext-method"></a>ReadText 方法
读取指定数目的字符来自文本[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>Parameters  
 *Numchar*  
 可选。 A**长**值，该值指定要从文件读取的字符数或[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)值。 默认值是**adReadAll**。  
  
## <a name="return-value"></a>返回值  
 **ReadText**方法读取指定的数目的字符、 一整行或从整个流**流**对象并返回结果字符串。  
  
## <a name="remarks"></a>Remarks  
 如果*保留的 NumChar*的字符数超过留在流中，将返回仅剩余字符。 读取的字符串没有字节可读取指定的长度*保留的 NumChar*。 如果没有留下可供读取的字符，则返回一个变体，其值为 null。 **ReadText**无法用于向后读取。  
  
> [!NOTE]
>  **ReadText**与文本流中使用方法 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 为二进制流 (**类型**是**adTypeBinary**)，使用[读取](../../../ado/reference/ado-api/read-method.md)。  
  
 导致大量的通过返回的 XML 数据的查询**ReadText** ActiveX 数据对象 (ADO) 流对象的方法可能需要大量时间来执行; 如果在从调用的 COM + 组件中执行此操作ASP 页上，用户的会话可能会超时。ADO 将从 utf-8 编码为 Unicode; 转换流对象数据经常性内存重新分配中如此大的数据的转换涉及是数量的非常耗时。 若要解决，请重复的调用**ReadText** ADO 方法命令对象，并指定较小数目的字符。 测试已显示的值等效于 128 K (131,072) 是最佳。 响应时间会降低，因为小于此值。 有关详细信息，请参阅知识库文章 280067，"PRB： 使用 ADO 流对象 ReadText 方法从 SQL Server 2000 检索非常大的 XML 文档可能会很慢"，在 Microsoft 知识库文章在 http://support.microsoft.com 。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Read 方法](../../../ado/reference/ado-api/read-method.md)
