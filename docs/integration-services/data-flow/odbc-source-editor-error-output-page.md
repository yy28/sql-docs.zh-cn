---
title: "ODBC 源编辑器（“错误输出”页） | Microsoft Docs"
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
  - "sql13.ssis.designer.odbcsource.errorhandling.f1"
ms.assetid: b2f6866c-db07-4cb3-9f38-889f8d2b03e6
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# ODBC 源编辑器（“错误输出”页）
  可以使用 **“ODBC 源编辑器”** 对话框的 **“错误输出”** 页选择错误处理选项。  
  
 若要了解有关 ODBC 源的详细信息，请参阅 [CDC Source](../../integration-services/data-flow/cdc-source.md)。  
  
## 任务列表  
 **打开“ODBC 源编辑器”的“错误输出”页**  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开具有 ODBC 源的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 包。  
  
-   在“数据流”选项卡上，双击 ODBC 源。  
  
-   在 **“ODBC 源编辑器”**中，单击 **“错误输出”**。  
  
## 选项  
  
### 输入/输出  
 查看数据源的名称。  
  
### 列  
 未使用。  
  
### 错误  
 选择 ODBC 源应该如何处理流中的错误：忽略失败、重定向行或使组件失败。  
  
### 截断  
 选择 ODBC 源应该如何处理流中的截断：忽略失败、重定向行或使组件失败。  
  
### Description  
 未使用。  
  
### 将此值设置到选定的单元格  
 选择发生错误或截断时 ODBC 源应如何处理所有选定的单元格：忽略失败、重定向行或使组件失败。  
  
### 应用  
 将错误处理选项应用到选定的单元格。  
  
## 错误处理选项  
 使用下列选项来配置 ODBC 源处理错误和截断的方式。  
  
### 组件失败  
 发生错误或截断时数据流任务失败。 这是默认行为。  
  
### 忽略失败  
 忽略错误或截断。  
  
### 重定向流  
 将引起错误或截断的行定向到 ODBC 源的错误输出。 有关详细信息，请参阅 [ODBC Source](../../integration-services/data-flow/odbc-source.md)。  
  
## 另请参阅  
 [ODBC 源编辑器（“连接管理器”页）](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)   
 [ODBC 源编辑器（“列”页）](../../integration-services/data-flow/odbc-source-editor-columns-page.md)  
  
  