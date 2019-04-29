---
title: 查找转换编辑器 （列页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.columns.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: 690ffef5-fd59-4e95-a27d-4fcf0d6b1c0b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 63410531bcb0af8a254b2d2a5c6c650423cb9a1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62890513"
---
# <a name="lookup-transformation-editor-columns-page"></a>查找转换编辑器（“列”页）
  可以使用 **“查找转换编辑器”** 对话框的 **“列”** 页，指定源表与引用表之间的联接以及从引用表中选择查找列。  
  
 若要了解有关查找转换的详细信息，请参阅 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)。  
  
## <a name="options"></a>选项  
 **可用输入列**  
 查看可用输入列的列表。 输入列是所连接源的数据流中的列。 输入列和查找列必须具有相互匹配的数据类型。  
  
 使用拖放操作将可用输入列映射到查找列。  
  
 还可以用键盘通过以下方法将输入列映射到查找列：突出显示 **“可用输入列”** 表中的某一列，按应用程序键，然后单击 **“编辑映射”**。  
  
 **可用查找列**  
 查看查找列的列表。 查找列是包含在引用表中并可在其中查找与输入列相匹配的值的列。  
  
 使用拖放操作将可用查找列映射到输入列。  
  
 使用这些复选框可以在引用表中选择要对其执行查找操作的列。  
  
 还可以用键盘通过以下方法将查找列映射到输入列：突出显示 **“可用查找列”** 表中的某一列，按应用程序键，然后单击 **“编辑映射”**。  
  
 **查找列**  
 查看所选的查找列。 通过选中 **“可用查找列”** 表中的复选框即可选择查找列。  
  
 **查找操作**  
 从列表中选择要对查找列执行的查找操作。  
  
 **输出别名**  
 为每个查找列的输出键入一个别名。 默认值为查找列的名称；不过，您也可以任选一个唯一的描述性名称。  
  
## <a name="see-also"></a>请参阅  
 [查找转换编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)   
 [查找转换编辑器（“连接”页）](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [查找转换编辑器（“高级”页）](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [查找转换编辑器（“错误输出”页）](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [模糊查找转换](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
