---
title: 查找转换编辑器 （错误输出页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.erroroutput.f1
ms.assetid: 15d53bb0-8be1-46fb-b459-04a397e75fac
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c9d2417c844998547480a2f03f6dcf9409ff7656
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767289"
---
# <a name="lookup-transformation-editor-error-output-page"></a>查找转换编辑器（“错误输出”页）
  可以使用 **“查找转换编辑器”** 对话框的 **“错误输出”** 页指定错误处理选项。  
  
 若要了解有关查找转换的详细信息，请参阅 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)。  
  
## <a name="options"></a>选项  
 **输入/输出**  
 查看输入的名称。  
  
 **列**  
 未使用。  
  
 **错误**  
 指定当处理在引用数据集内没有匹配项的行时应当出现的错误类型：  
  
-   忽略该失败并将行定向到输出。  
  
-   将行重定向到错误输出。  
  
-   使组件失败。  
  
 如果您在 **“指定如何处理无匹配项的行** 列表中选中了 **“将行重定向到无匹配输出”** ，则该选项不可用。 此列表位于 **“查找转换编辑器”** 对话框的 **“常规”** 页上。  
  
 **相关主题：**[数据中的错误处理](data-flow/error-handling-in-data.md)  
  
 **截断**  
 指定在发生数据截断时应当出现的情况：  
  
-   忽略失败。  
  
-   重定向行。  
  
-   使组件失败。  
  
 **说明**  
 查看操作的说明。  
  
 **将选定的单元格设置为此值**  
 指定在发生错误或截断时，选定的所有单元格应当出现的情况：  
  
-   忽略失败。  
  
-   重定向行。  
  
-   使组件失败。  
  
 **应用**  
 将错误处理选项应用到选定的单元格。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
