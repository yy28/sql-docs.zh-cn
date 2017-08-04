---
title: "ODBC 目标编辑器 （错误输出页） |Microsoft 文档"
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
- sql13.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e0fa59290399f3c3f7fc42b1f74b6a42c573f7d2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="odbc-destination-editor-error-output-page"></a>ODBC 目标编辑器（“错误输出”页）
  可以使用 **“ODBC 目标编辑器”** 对话框的 **“错误输出”** 页选择错误处理选项。  
  
 若要了解有关 ODBC 目标的详细信息，请参阅 [ODBC Destination](../../integration-services/data-flow/odbc-destination.md)。  
  
 **打开 ODBC 目标编辑器的“错误输出”页**  
  
## <a name="task-list"></a>任务列表  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开包含 ODBC 目标的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 包。  
  
-   在“数据流”选项卡上，双击 ODBC 目标。  
  
-   在 **“ODBC 目标编辑器”**中，单击 **“错误输出”**。  
  
## <a name="options"></a>选项  
  
### <a name="inputoutput"></a>输入/输出  
 查看数据源的名称。  
  
### <a name="column"></a>列  
 未使用。  
  
### <a name="error"></a>错误  
 选择 ODBC 目标应该如何处理流中的错误：忽略失败、重定向行或使组件失败。  
  
### <a name="truncation"></a>截断  
 选择 ODBC 目标应该如何处理流中的截断：忽略失败、重定向行或使组件失败。  
  
### <a name="description"></a>Description  
 查看错误说明。  
  
### <a name="set-this-value-to-selected-cells"></a>将此值设置到选定的单元格  
 选择发生错误或截断时 ODBC 目标应如何处理所有选定的单元格：忽略失败、重定向行或使组件失败。  
  
### <a name="apply"></a>应用  
 将错误处理选项应用到选定的单元格。  
  
## <a name="error-handling-options"></a>错误处理选项  
 使用下列选项来配置 ODBC 目标处理错误和截断的方式。  
  
### <a name="fail-component"></a>组件失败  
 发生错误或截断时数据流任务失败。 这是默认行为。  
  
### <a name="ignore-failure"></a>忽略失败  
 忽略错误或截断。  
  
### <a name="redirect-flow"></a>重定向流  
 将引起错误或截断的行定向到 ODBC 目标的错误输出。 有关详细信息，请参阅 ODBC 目标。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 目标编辑器 &#40;连接管理器页 &#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [ODBC 目标编辑器 &#40;映射页 &#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
  
