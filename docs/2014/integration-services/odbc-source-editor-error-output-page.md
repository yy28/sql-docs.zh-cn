---
title: ODBC 源编辑器 （错误输出页） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: b2f6866c-db07-4cb3-9f38-889f8d2b03e6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1bf6d22a2cbe6111f9cce1a3be446c507969ca82
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158417"
---
# <a name="odbc-source-editor-error-output-page"></a>ODBC 源编辑器（“错误输出”页）
  可以使用 **“ODBC 源编辑器”** 对话框的 **“错误输出”** 页选择错误处理选项。  
  
 若要了解有关 ODBC 源的详细信息，请参阅 [CDC Source](data-flow/cdc-source.md)。  
  
## <a name="task-list"></a>任务列表  
 **打开“ODBC 源编辑器”的“错误输出”页**  
  
-   在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，打开具有 ODBC 源的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 包。  
  
-   在“数据流”选项卡上，双击 ODBC 源。  
  
-   在 **“ODBC 源编辑器”** 中，单击 **“错误输出”**。  
  
## <a name="options"></a>选项  
  
### <a name="inputoutput"></a>输入/输出  
 查看数据源的名称。  
  
### <a name="column"></a>“列”  
 未使用。  
  
### <a name="error"></a>错误  
 选择 ODBC 源应该如何处理流中的错误：忽略失败、重定向行或使组件失败。  
  
### <a name="truncation"></a>截断  
 选择 ODBC 源应该如何处理流中的截断：忽略失败、重定向行或使组件失败。  
  
### <a name="description"></a>Description  
 未使用。  
  
### <a name="set-this-value-to-selected-cells"></a>将此值设置到选定的单元格  
 选择发生错误或截断时 ODBC 源应如何处理所有选定的单元格：忽略失败、重定向行或使组件失败。  
  
### <a name="apply"></a>应用  
 将错误处理选项应用到选定的单元格。  
  
## <a name="error-handling-options"></a>错误处理选项  
 使用下列选项来配置 ODBC 源处理错误和截断的方式。  
  
### <a name="fail-component"></a>组件失败  
 发生错误或截断时数据流任务失败。 这是默认行为。  
  
### <a name="ignore-failure"></a>忽略失败  
 忽略错误或截断。  
  
### <a name="redirect-flow"></a>重定向流  
 将引起错误或截断的行定向到 ODBC 源的错误输出。 有关详细信息，请参阅 [ODBC Source](data-flow/odbc-source.md)。  
  
## <a name="see-also"></a>请参阅  
 [ODBC 源编辑器&#40;连接管理器页&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [ODBC 源编辑器&#40;列页&#41;](../../2014/integration-services/odbc-source-editor-columns-page.md)  
  
  
