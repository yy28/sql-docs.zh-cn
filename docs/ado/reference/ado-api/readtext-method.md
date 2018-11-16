---
title: ReadText 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b095e034df987fd580b5f5855993c9cf070a1236
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51599838"
---
# <a name="readtext-method"></a>ReadText 方法
读取指定数目的字符从短信[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>Parameters  
 *numChars*  
 可选。 一个**长**值，该值指定要从文件中读取的字符数或[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)值。 默认值是**adReadAll**。  
  
## <a name="return-value"></a>返回值  
 **ReadText**方法读取指定的数量的字符、 一整行或从整个流**Stream**对象并返回生成的字符串。  
  
## <a name="remarks"></a>备注  
 如果*NumChar*个以上的字符数留在流中，返回的剩余字符。 读取的字符串不填充以匹配指定的长度*NumChar*。 如果有没有留下供读取的字符，则返回值为 null 的变体。 **ReadText**不能用于向后读取。  
  
> [!NOTE]
>  **ReadText**方法使用文本流 ([类型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 对于二进制流 (**类型**是**adTypeBinary**)，使用[读取](../../../ado/reference/ado-api/read-method.md)。  
  
 导致大量的通过返回的 XML 数据的查询**ReadText** ActiveX 数据对象 (ADO) Stream 对象的方法可能需要大量时间来执行; 如果这是在从调用在 COM + 组件ASP 页上，用户的会话可能会超时。ADO Stream 对象数据将从 utf-8 编码转换到 Unicode;经常性内存重新分配操作所涉及如此大的数据的转换是数量的非常耗时。 若要解决，请重复的调用**ReadText**方法 ADO 命令对象，并指定较小数目的字符。 测试已表明 128 K (131,072) 与等效的值是最佳。 随着减小该值，而减少响应时间。 有关详细信息，请参阅知识库文章 280067，"PRB： 使用 ADO 流对象 ReadText 方法从 SQL Server 2000 检索非常大的 XML 文档可能会很慢"，在 Microsoft 知识库文章在 https://support.microsoft.com 。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Read 方法](../../../ado/reference/ado-api/read-method.md)
