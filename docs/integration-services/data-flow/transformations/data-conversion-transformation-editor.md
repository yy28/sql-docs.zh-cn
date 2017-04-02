---
title: "数据转换编辑器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dataconversiontransformation.f1"
helpviewer_keywords: 
  - "数据转换编辑器"
ms.assetid: 7b4e4873-e8fe-4549-a965-65bebdb270bc
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# 数据转换编辑器
  可以使用 **“数据转换编辑器”** 对话框，选择要转换的列和要将列转换成的数据类型以及设置转换属性。  
  
> [!NOTE]  
>  数据转换的输出列的 **FastParse** 属性未在 **“数据转换编辑器”**中提供，但可以使用 **“高级编辑器”**进行设置。 有关此属性的详细信息，请参阅 [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)的“数据转换”部分。  
  
 若要了解有关数据转换的详细信息，请参阅 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)。  
  
## 选项  
 **可用输入列**  
 使用复选框选择要转换的列。 选择后，会将输入列添加到下表中。  
  
 **输入列**  
 从可用输入列的列表中选择要转换的列。 通过选中上述相应的复选框即可选择输入列。  
  
 **输出别名**  
 为每一个新列键入一个别名。 默认为 **Copy of** 后接输入列名。不过，你也可以任选一个唯一的描述性名称。  
  
 **数据类型**  
 从列表中选择可用的数据类型。 有关详细信息，请参阅 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)。  
  
 **长度**  
 设置字符串数据的列长度。  
  
 **精度**  
 设置数字数据的精度。  
  
 **小数位数**  
 设置数字数据的小数位数。  
  
 **代码页**  
 为 DT_STR 类型的列选择相应的代码页。  
  
 **配置错误输出**  
 使用[配置错误输出](../Topic/Configure%20Error%20Output.md)对话框指定处理行级错误的方式。  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)   
 [使用数据转换将数据转换为其他数据类型](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)  
  
  