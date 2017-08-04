---
title: "字符映射表转换 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.charactertrans.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 80818df1eb99cfe68012a119d4482698b17d0044
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="character-map-transformation"></a>字符映射表转换
  字符映射表转换将字符串函数（如从小写到大写的转换）应用于字符数据。 此转换操作只对字符串数据类型的列数据执行。  
  
 字符映射表转换可就地转换列数据，也可添加一个转换输出列，将转换后的数据放到新列中。 可以对同一输入列应用一组不同的映射操作，并将结果放到不同的列中。 例如，可对同一列进行大写和小写转换，并将结果放到两个不同列中。  
  
 某些情况下，映射可能导致数据被截断。 例如，如果将单字节字符映射到采用多字节表示形式的字符，则可能发生截断。 字符映射表转换包含一个错误输出，可用于将截断的数据定向到单独的输出。 有关详细信息，请参阅 [数据中的错误处理](../../../integration-services/data-flow/error-handling-in-data.md)。  
  
 此转换有一个输入、一个输出和一个错误输出。  
  
## <a name="mapping-operations"></a>映射操作  
 下表说明了字符映射表转换支持的映射操作。  
  
|运算|Description|  
|---------------|-----------------|  
|Byte reversal|反转字节顺序。|  
|Full width|将半角字符映射到全角字符。|  
|Half width|将全角字符映射到半角字符。|  
|Hiragana|将片假名字符映射到平假名字符。|  
|Katakana|将平假名字符映射到片假名字符。|  
|Linguistic casing|应用语言中的大小写来取代系统规则。 语言中的大小写是指 Win32 API 为 Turkic 和其他区域设置的 Unicode 简单大小写映射提供的功能。|  
|Lowercase|将字符转换为小写。|  
|简体中文|将繁体中文字符映射到简体中文字符。|  
|繁体中文|将简体中文字符映射到繁体中文字符。|  
|大写|将字符转换为大写。|  
  
## <a name="mutually-exclusive-mapping-operations"></a>互相排斥的映射操作  
 一次转换可以执行多个操作。 但是，有些映射操作是互相排斥的。 下表列出了对同一个列使用多个操作时适用的限制。 操作 A 列和操作 B 列中的操作是互相排斥的。  
  
|操作 A|操作 B|  
|-----------------|-----------------|  
|Lowercase|大写|  
|Hiragana|Katakana|  
|Half width|Full width|  
|繁体中文|简体中文|  
|Lowercase|Hiragana、katakana、half width、full width|  
|大写|Hiragana、katakana、half width、full width|  
  
## <a name="configuration-of-the-character-map-transformation"></a>配置字符映射表转换  
 可以采用下列方法来配置字符映射表转换：  
  
-   指定要转换的列。  
  
-   指定要应用于每一列的操作。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 **“字符映射表转换编辑器”** 对话框中设置的属性的详细信息，请参阅 [Character Map Transformation Editor](../../../integration-services/data-flow/transformations/character-map-transformation-editor.md)。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请单击下列主题之一：  
  
-   [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [为合并转换和合并联接转换排序数据](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
  
