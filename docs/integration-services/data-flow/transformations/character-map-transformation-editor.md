---
title: "字符映射表转换编辑器 |Microsoft 文档"
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
- sql13.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- Character Map Transformation Editor
ms.assetid: 3f1dbcf9-9cca-4606-bdcc-7ea6ad48cdf3
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1ddabff7405401657b44a4cbc9205cf6092949d7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="character-map-transformation-editor"></a>字符映射表转换编辑器
  可以使用“字符映射表转换编辑器”对话框，选择要应用到列数据的字符串函数，以及指定映射是就地更改还是添加为新列。  
  
 若要了解有关字符映射表转换的详细信息，请参阅 [Character Map Transformation](../../../integration-services/data-flow/transformations/character-map-transformation.md)。  
  
## <a name="options"></a>选项  
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
 使用“配置错误输出” [](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 对话框可以为此转换指定错误处理选项。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  
