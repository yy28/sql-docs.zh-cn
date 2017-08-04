---
title: "CDC 源编辑器 （列页） |Microsoft 文档"
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
- sql13.ssis.designer.cdcsource.columns.f1
ms.assetid: bcf3030e-98d8-4445-967c-33c3f8ecb4fc
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c746e2b90c9f4f2fc34a9285cf05612302e5c588
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="cdc-source-editor-columns-page"></a>CDC 源编辑器（“列”页）
  可以使用“CDC 源编辑器”对话框的“列”页，将输出列映射到每个外部（源）列。  
  
 若要了解有关 CDC 源的详细信息，请参阅 [CDC Source](../../integration-services/data-flow/cdc-source.md)。  
  
## <a name="task-list"></a>任务列表  
 **打开“CDC 源编辑器”的“列”页**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开具有 CDC 源的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 CDC 源。  
  
3.  在 **“CDC 源编辑器”**中，单击 **“列”**。  
  
## <a name="options"></a>选项  
 **可用外部列**  
 数据源中的可用外部列的列表。 无法使用此表添加或删除列。 在源中选择要使用的列。 所选列将按照选择它们时的顺序添加到 **“外部列”** 列表中。  
  
 **“外部列”**  
 外部（源）列的视图，该视图按照您在配置使用 CDC 源中数据的组件时所看到的列顺序显示。 若要更改此顺序，请首先清除 **“可用外部列”** 列表中所选的列，然后以不同的顺序从列表中选择外部列。 所选列将按照选择它们时的顺序添加到 **“外部列”** 列表中。  
  
 **输出列**  
 输入每个输出列的唯一名称。 默认值为所选外部（源）列的名称，不过，也可以任选一个唯一的描述性名称。 输入的名称显示在 SSIS 设计器中。  
  
## <a name="see-also"></a>另请参阅  
 [CDC 源编辑器 &#40;连接管理器页 &#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)   
 [CDC 源编辑器 &#40;错误输出页 &#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
  
