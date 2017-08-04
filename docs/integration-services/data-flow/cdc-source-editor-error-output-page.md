---
title: "CDC 源编辑器 （错误输出页） |Microsoft 文档"
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
- sql13.ssis.designer.cdcsource.errorhandling.f1
ms.assetid: 8a4c2cb8-fd2f-4c45-824f-b93473a8981e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 15818f42922d7fe21bdba64d0bf4c5e4a593eada
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="cdc-source-editor-error-output-page"></a>CDC 源编辑器（“错误输出”页）
  可以使用 **“CDC 源编辑器”** 对话框的 **“错误输出”** 页选择错误处理选项。  
  
 若要了解有关 CDC 源的详细信息，请参阅 [CDC Source](../../integration-services/data-flow/cdc-source.md)。  
  
## <a name="task-list"></a>任务列表  
 **打开“CDC 源编辑器”的“错误输出”页**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开具有 CDC 源的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 CDC 源。  
  
3.  在 **“CDC 源编辑器”**中，单击 **“错误输出”**。  
  
## <a name="options"></a>选项  
 **输入/输出**  
 查看数据源的名称。  
  
 **列**  
 查看在“CDC 源编辑器”对话框中“连接管理器”页上选择的外部（源）列。  
  
 **错误**  
 选择 CDC 源应该如何处理流中的错误：忽略失败、重定向行或使组件失败。  
  
 **截断**  
 选择 CDC 源应该如何处理流中的截断：忽略失败、重定向行或使组件失败。  
  
 **Description**  
 未使用。  
  
 **将此值设置到选定的单元格**  
 选择发生错误或截断时 CDC 源应如何处理所有选定的单元格：忽略失败、重定向行或使组件失败。  
  
 **应用**  
 将错误处理选项应用到选定的单元格。  
  
## <a name="error-handling-options"></a>错误处理选项  
 使用下列选项来配置 CDC 源处理错误和截断的方式。  
  
 **组件失败**  
 发生错误或截断时数据流任务失败。 这是默认行为。  
  
 **忽略失败**  
 忽略错误或截断，并且将数据行定向到 CDC 源输出。  
  
 **重定向流**  
 错误或截断数据行定向到 CDC 源的错误输出。 在此情况下使用 CDC 源错误处理。 有关详细信息，请参阅 [CDC Source](../../integration-services/data-flow/cdc-source.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CDC 源编辑器 &#40;连接管理器页 &#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)   
 [CDC 源编辑器 &#40;列页 &#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)  
  
  
