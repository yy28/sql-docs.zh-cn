---
title: "导出列转换编辑器 （列页） |Microsoft 文档"
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
- sql13.dts.designer.fileextractortransformation.columns.f1
helpviewer_keywords:
- Export Column Transformation Editor
ms.assetid: b659a5c2-5509-4b5b-9c82-136c971d5c7f
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e3538e9379c48faaa700f56aa1ecf0ceafc68e2a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="export-column-transformation-editor-columns-page"></a>导出列转换编辑器（“列”页）
  可以使用 **“导出列转换编辑器”** 对话框的 **“列”** 页，指定数据流中要提取到文件的列。 可以指定导出列转换是将数据追加到文件还是覆盖现有文件。  
  
 若要了解有关导出列转换的详细信息，请参阅 [Export Column Transformation](../../../integration-services/data-flow/transformations/export-column-transformation.md)。  
  
## <a name="options"></a>选项  
 **提取列**  
 从包含文本数据或图像数据的输入列的列表中进行选择。 所有行都应包含 **“提取列”** 和 **“文件路径列”**的定义。  
  
 **“文件路径列”**  
 从包含文件路径和文件名的输入列的列表中进行选择。 所有行都应包含 **“提取列”** 和 **“文件路径列”**的定义。  
  
 **允许追加**  
 指定转换是否将数据追加到现有文件。 默认值为 **false**。  
  
 **强制截断**  
 指定转换在写入数据之前是否删除现有文件的内容。 默认值为 **false**。  
  
 **写入 BOM**  
 指定是否将字节顺序标记 (BOM) 写入文件。 只有在数据具有 **DT_NTEXT** 或 DT_WSTR 数据类型，并且未将数据追加到现有数据文件时，才会写入 BOM。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)   
 [导出列转换编辑器 &#40;错误输出页 &#41;](../../../integration-services/data-flow/transformations/export-column-transformation-editor-error-output-page.md)  
  
  
