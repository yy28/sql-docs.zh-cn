---
title: 字词查找转换编辑器（"字词查找" 选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termlookup.termlookup.f1
helpviewer_keywords:
- Term Lookup Transformation Editor
ms.assetid: 245d3466-d51f-4073-978a-694a8d9dfaec
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d67c8c02e79583b5c8f4295abc4d71c2b05dae8b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962070"
---
# <a name="term-lookup-transformation-editor-term-lookup-tab"></a>字词查找转换编辑器（“字词查找”选项卡）
  可以使用 **“字词查找转换编辑器”** 对话框的 **“字词查找”** 选项卡，将输入列映射到引用表中的查找列，以及为每个输出列提供别名。  
  
 若要了解有关字词查找转换的详细信息，请参阅 [Term Lookup Transformation](data-flow/transformations/lookup-transformation.md)。  
  
## <a name="options"></a>选项  
 **可用输入列**  
 使用复选框选择要传递给未更改输出的输入列。 将输入列拖动到 **“可用引用列”** 列表可以将其映射到引用表中的查找列。 输入列和查找列必须具有支持的匹配数据类型（DT_NTEXT 或 DT_WSTR）。 选择一个映射行，再右键单击可在 [创建关系](data-flow/transformations/create-relationships.md) 对话框中编辑该映射。  
  
 **“可用引用列”**  
 查看引用表中可用的列。 选择包含要匹配的字词列表的列。  
  
 **传递列**  
 从可用输入列的列表中进行选择。 通过选中 **“可用输入列”** 表中的复选框来选择列。  
  
 **输出列别名**  
 为每个输出列键入一个别名。 默认值为列的名称；不过，您也可以任选一个唯一的描述性名称。  
  
 **配置错误输出**  
 使用 [配置错误输出](../../2014/integration-services/configure-error-output.md) 对话框可以为导致错误的行指定错误处理方式选项。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [字词查找转换编辑器 &#40;引用表 "选项卡&#41;](../../2014/integration-services/term-lookup-transformation-editor-reference-table-tab.md)   
 [字词查找转换编辑器 &#40;高级 "选项卡&#41;](../../2014/integration-services/term-lookup-transformation-editor-advanced-tab.md)   
 [字词提取转换](data-flow/transformations/term-extraction-transformation.md)  
  
  
