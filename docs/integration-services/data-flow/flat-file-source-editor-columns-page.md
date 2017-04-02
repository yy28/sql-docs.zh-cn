---
title: "平面文件源编辑器（“列”页） | Microsoft Docs"
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
  - "sql13.dts.designer.flatfilesourceadapter.columns.f1"
helpviewer_keywords: 
  - "平面文件源编辑器"
ms.assetid: b5af5f65-c087-44fd-b5ae-d0441245fef2
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# 平面文件源编辑器（“列”页）
  可以使用“平面文件源编辑器”对话框的“列”节点，将输出列映射到每个外部（源）列。  
  
> [!NOTE]  
>  平面文件源的 **FileNameColumnName** 属性及其输出列的 **FastParse** 属性未在 **“平面文件源编辑器”**中提供，但可以使用 **“高级编辑器”**进行设置。 有关这些属性的详细信息，请参阅 [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md)的“平面文件源”部分。  
  
 若要了解有关平面文件源的详细信息，请参阅 [Flat File Source](../../integration-services/data-flow/flat-file-source.md)。  
  
## 选项  
 **可用外部列**  
 查看数据源中可用外部列的列表。 无法使用此表添加或删除列。  
  
 **“外部列”**  
 按任务读取外部（源）列的顺序查看这些列。 首先清除表中所选的列，然后以不同的顺序从列表中选择外部列，即可更改顺序。  
  
 **输出列**  
 为每个输出列提供唯一的名称。 默认值为所选外部（源）列的名称；不过，您也可以任选一个唯一的描述性名称。 所提供的名称将在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中显示。  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [平面文件源编辑器（“连接管理器”页）](../../integration-services/data-flow/flat-file-source-editor-connection-manager-page.md)   
 [平面文件源编辑器（“错误输出”页）](../../integration-services/data-flow/flat-file-source-editor-error-output-page.md)   
 [平面文件连接管理器](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  