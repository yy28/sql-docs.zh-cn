---
title: CDC 源编辑器（"错误输出" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.errorhandling.f1
ms.assetid: 8a4c2cb8-fd2f-4c45-824f-b93473a8981e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3bf33d52b380e1ac05864c6e7402567b42df54a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061043"
---
# <a name="cdc-source-editor-error-output-page"></a>CDC 源编辑器（“错误输出”页）
  可以使用 **“CDC 源编辑器”** 对话框的 **“错误输出”** 页选择错误处理选项。  
  
 若要了解有关 CDC 源的详细信息，请参阅 [CDC Source](data-flow/cdc-source.md)。  
  
## <a name="task-list"></a>任务列表  
 **打开“CDC 源编辑器”的“错误输出”页**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，打开具有 CDC 源的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 包。  
  
2.  在“数据流”**** 选项卡上，双击 CDC 源。  
  
3.  在 **“CDC 源编辑器”** 中，单击 **“错误输出”**。  
  
## <a name="options"></a>选项  
 **输入/输出**  
 查看数据源的名称。  
  
 **列**  
 查看在“CDC 源编辑器”**** 对话框中“连接管理器”**** 页上选择的外部（源）列。  
  
 **错误**  
 选择 CDC 源应该如何处理流中的错误：忽略失败、重定向行或使组件失败。  
  
 **截断**  
 选择 CDC 源应该如何处理流中的截断：忽略失败、重定向行或使组件失败。  
  
 **说明**  
 未使用。  
  
 **将此值设置到选定的单元格**  
 选择发生错误或截断时 CDC 源应如何处理所有选定的单元格：忽略失败、重定向行或使组件失败。  
  
 **应用**  
 将错误处理选项应用到选定的单元格。  
  
## <a name="error-handling-options"></a>错误处理选项  
 使用下列选项来配置 CDC 源处理错误和截断的方式。  
  
 **组件失败**  
 发生错误或截断时数据流任务失败。 此选项为默认行为。  
  
 **忽略失败**  
 忽略错误或截断，并且将数据行定向到 CDC 源输出。  
  
 **重定向流**  
 错误或截断数据行定向到 CDC 源的错误输出。 在此情况下使用 CDC 源错误处理。 有关详细信息，请参阅 [CDC Source](data-flow/cdc-source.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CDC 源编辑器 &#40;连接管理器页&#41;](../../2014/integration-services/cdc-source-editor-connection-manager-page.md)   
 [CDC 源编辑器（“列”页）](../../2014/integration-services/cdc-source-editor-columns-page.md)  
  
  
