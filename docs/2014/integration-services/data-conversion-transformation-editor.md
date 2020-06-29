---
title: 数据转换编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- Data Conversion Transformation Editor
ms.assetid: 7b4e4873-e8fe-4549-a965-65bebdb270bc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e68fb1edd69e20628baaeda8802ec712da7d5117
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432614"
---
# <a name="data-conversion-transformation-editor"></a>数据转换编辑器
  可以使用 **“数据转换编辑器”** 对话框，选择要转换的列和要将列转换成的数据类型以及设置转换属性。  
  
> [!NOTE]  
>  数据转换的 `FastParse` 输出列的属性在 "**数据转换编辑器**" 中不可用，但可以使用**高级编辑器**进行设置。 有关此属性的详细信息，请参阅 [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md)的“数据转换”部分。  
  
 若要了解有关数据转换的详细信息，请参阅 [Data Conversion Transformation](data-flow/transformations/data-conversion-transformation.md)。  
  
## <a name="options"></a>选项  
 **可用输入列**  
 使用复选框选择要转换的列。 选择后，会将输入列添加到下表中。  
  
 **输入列**  
 从可用输入列的列表中选择要转换的列。 通过选中上述相应的复选框即可选择输入列。  
  
 **输出别名**  
 为每一个新列键入一个别名。 默认为 `Copy of` 后接输入列名。不过，你也可以任选一个唯一的描述性名称。  
  
 **数据类型**  
 从列表中选择可用的数据类型。 有关详细信息，请参阅[Integration Services 数据类型](data-flow/integration-services-data-types.md)。  
  
 **长度**  
 设置字符串数据的列长度。  
  
 **精度**  
 设置数字数据的精度。  
  
 **缩放**  
 设置数字数据的小数位数。  
  
 **代码页**  
 为 DT_STR 类型的列选择相应的代码页。  
  
 **配置错误输出**  
 使用 [配置错误输出](../../2014/integration-services/configure-error-output.md) 对话框指定处理行级错误的方式。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用数据转换将数据转换为其他数据类型](data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)  
  
  
