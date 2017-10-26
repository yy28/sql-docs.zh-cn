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
- sql13.dts.designer.charactermaptransformation.f1
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: 3ea6f6f0526a0ad1a2f98c97aed2a7aebbffb65a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/19/2017

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
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请单击下列主题之一：  
  
-   [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [合并和合并联接转换对数据进行排序](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="character-map-transformation-editor"></a>字符映射表转换编辑器
  可以使用“字符映射表转换编辑器”对话框，选择要应用到列数据的字符串函数，以及指定映射是就地更改还是添加为新列。  
  
### <a name="options"></a>选项  
 **可用输入列**  
 使用该复选框可以选择通过字符串函数转换的列。 您的选择将显示在下表中。  
  
 **输入列**  
 查看从上表中选择的输入列。 您也可使用可用输入列的列表更改或删除选项。  
  
 **目标**  
 指定是否就地保存字符串运算结果、使用现有列或将已修改的数据作为新列保存。  
  
|“值”|Description|  
|-----------|-----------------|  
|新列|将数据保存在新列中。 在 **“输出别名”**下分配列名。|  
|就地更改|将已修改的数据保存在现有的列中。|  
  
 **运算**  
 从列表中选择要应用于列数据的字符串函数。  
  
|“值”|Description|  
|-----------|-----------------|  
|Lowercase|转换为小写字母。|  
|大写|转换为大写字母。|  
|Byte reversal|通过反转字节顺序进行转换。|  
|Hiragana|将日语的片假名字符转换为平假名字符。|  
|Katakana|将日语的平假名字符转换为片假名字符。|  
|Half width|将全角字符转换为半角字符。|  
|Full width|将半角字符转换为全角字符。|  
|Linguistic casing|应用大小写语言规则（为土耳其语和其他区域语言设置的 Unicode 简单大小写映射）而不是系统规则。|  
|简体中文|将繁体中文字符转换为简体中文字符。|  
|繁体中文|将简体中文字符转换为繁体中文字符。|  
  
 **“输出别名”**  
 为每个输出列键入一个别名。 默认为 **Copy of** 后接输入列名。不过，你也可以任选一个唯一的描述性名称。  
  
 **配置错误输出**  
 使用 “[配置错误输出](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9)” 对话框可以为此转换指定错误处理选项。  
  
  

