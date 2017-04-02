---
title: "Analysis Services 执行 DDL 任务编辑器（DDL 页） | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.asexecuteddltask.ddl.f1"
helpviewer_keywords: 
  - "Analysis Services 执行 DDL 任务编辑器"
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Analysis Services 执行 DDL 任务编辑器（DDL 页）
  可以使用“Analysis Services 执行 DDL 任务编辑器”对话框的 **DDL** 页指定与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的连接，以及提供有关数据定义语言 (DDL) 语句的源的信息。  
  
 若要了解此任务，请参阅 [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)。  
  
## 静态选项  
 **连接**  
 在列表中选择 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接管理器，或单击“\<新建连接...>”并使用“添加 Analysis Services 连接管理器”对话框新建一个连接。  
  
 **相关主题：**[“添加 Analysis Services 连接管理器”对话框 UI 参考](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)、[Analysis Services 连接管理器](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 指定 DDL 语句的源类型。 此属性具有下表所列的选项：  
  
|“值”|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为 **SourceDirect** 文本框中存储的 DDL 语句。 选择此值将显示以下部分中的动态选项。|  
|**文件连接**|将源设置为包含 DDL 语句的文件。 选择此值将显示以下部分中的动态选项。|  
|**变量**|将源设置为变量。 选择此值将显示以下部分中的动态选项。|  
  
## 动态选项  
  
### SourceType = 直接输入  
 **数据源**  
 键入 DDL 语句，或单击省略号 **(…)**，然后在“DDL 语句”对话框中键入语句。  
  
### SourceType = 文件连接  
 **数据源**  
 在列表中选择“文件连接”，或单击“\<新建连接...>”并使用“文件连接管理器”对话框新建一个连接。  
  
 **相关主题：**[文件连接管理器](../../integration-services/connection-manager/file-connection-manager.md)  
  
### SourceType = 变量  
 **数据源**  
 在列表中选择一个变量，或单击“\<新建连接...>”并使用“添加变量”对话框新建一个变量。  
  
 **相关主题：**[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services 执行 DDL 任务编辑器（“常规”页）](../../integration-services/control-flow/analysis-services-execute-ddl-task-editor-general-page.md)   
 [“表达式”页](../../integration-services/expressions/expressions-page.md)   
 [控制流](../../integration-services/control-flow/control-flow.md)   
 [Analysis Services 脚本语言（支持 XMLA 的 ASSL）](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [XML for Analysis (XMLA) 参考](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  