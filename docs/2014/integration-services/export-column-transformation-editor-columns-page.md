---
title: 导出列转换编辑器 （列页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fileextractortransformation.columns.f1
helpviewer_keywords:
- Export Column Transformation Editor
ms.assetid: b659a5c2-5509-4b5b-9c82-136c971d5c7f
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e12fa5ca9d9295ffe1311062215217044ada2135
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048387"
---
# <a name="export-column-transformation-editor-columns-page"></a>导出列转换编辑器（“列”页）
  可以使用 **“导出列转换编辑器”** 对话框的 **“列”** 页，指定数据流中要提取到文件的列。 可以指定导出列转换是将数据追加到文件还是覆盖现有文件。  
  
 若要了解有关导出列转换的详细信息，请参阅 [Export Column Transformation](data-flow/transformations/export-column-transformation.md)。  
  
## <a name="options"></a>选项  
 **提取列**  
 从包含文本数据或图像数据的输入列的列表中进行选择。 所有行都应包含 **“提取列”** 和 **“文件路径列”** 的定义。  
  
 **“文件路径列”**  
 从包含文件路径和文件名的输入列的列表中进行选择。 所有行都应包含 **“提取列”** 和 **“文件路径列”** 的定义。  
  
 **允许追加**  
 指定转换是否将数据追加到现有文件。 默认值为 `false`。  
  
 **强制截断**  
 指定转换在写入数据之前是否删除现有文件的内容。 默认值为 `false`。  
  
 **写入 BOM**  
 指定是否将字节顺序标记 (BOM) 写入文件。 数据是否仅写入 BOM`DT_NTEXT`或 DT_WSTR 数据类型，并不会追加到现有数据文件。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [导出列转换编辑器&#40;错误输出页&#41;](../../2014/integration-services/export-column-transformation-editor-error-output-page.md)  
  
  
