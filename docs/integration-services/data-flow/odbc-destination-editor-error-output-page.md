---
title: "ODBC 目标编辑器（“错误输出”页） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.odbcdest.errorhandling.f1"
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# ODBC 目标编辑器（“错误输出”页）
  可以使用 **“ODBC 目标编辑器”** 对话框的 **“错误输出”** 页选择错误处理选项。  
  
 若要了解有关 ODBC 目标的详细信息，请参阅 [ODBC Destination](../../integration-services/data-flow/odbc-destination.md)。  
  
 **打开 ODBC 目标编辑器的“错误输出”页**  
  
## 任务列表  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开包含 ODBC 目标的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 包。  
  
-   在“数据流”选项卡上，双击 ODBC 目标。  
  
-   在 **“ODBC 目标编辑器”**中，单击 **“错误输出”**。  
  
## 选项  
  
### 输入/输出  
 查看数据源的名称。  
  
### 列  
 未使用。  
  
### 错误  
 选择 ODBC 目标应该如何处理流中的错误：忽略失败、重定向行或使组件失败。  
  
### 截断  
 选择 ODBC 目标应该如何处理流中的截断：忽略失败、重定向行或使组件失败。  
  
### Description  
 查看错误说明。  
  
### 将此值设置到选定的单元格  
 选择发生错误或截断时 ODBC 目标应如何处理所有选定的单元格：忽略失败、重定向行或使组件失败。  
  
### 应用  
 将错误处理选项应用到选定的单元格。  
  
## 错误处理选项  
 使用下列选项来配置 ODBC 目标处理错误和截断的方式。  
  
### 组件失败  
 发生错误或截断时数据流任务失败。 这是默认行为。  
  
### 忽略失败  
 忽略错误或截断。  
  
### 重定向流  
 将引起错误或截断的行定向到 ODBC 目标的错误输出。 有关详细信息，请参阅 ODBC 目标。  
  
## 另请参阅  
 [ODBC 目标编辑器（“连接管理器”页）](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [ODBC 目标编辑器（“映射”页）](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
  