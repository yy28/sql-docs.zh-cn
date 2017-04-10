---
title: "平面文件目标编辑器（“连接管理器”页） | Microsoft Docs"
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
  - "sql13.dts.designer.flatfiledestadapter.connection.f1"
helpviewer_keywords: 
  - "平面文件目标编辑器"
ms.assetid: b01571fa-bc19-4742-8eed-ac163172a919
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# 平面文件目标编辑器（“连接管理器”页）
  可以使用 **“平面文件目标编辑器”** 对话框的 **“连接管理器”** 页为目标选择平面文件连接，以及指定是覆盖现有目标文件还是追加到现有目标文件。 平面文件目标可以将数据写入文本文件。 该文本文件可以采用带分隔符、固定宽度、带有行分隔符的固定宽度或右边未对齐的格式。  
  
 若要了解有关平面文件目标的详细信息，请参阅 [Flat File Destination](../../integration-services/data-flow/flat-file-destination.md)。  
  
## 选项  
 **平面文件连接管理器**  
 使用列表框选择现有的连接管理器，或单击“新建”创建新的连接管理器。  
  
 **新建**  
 使用“平面文件格式”和“平面文件连接管理器编辑器”对话框创建新的连接。  
  
 **“平面文件格式”** 对话框中除了提供带分隔符、固定宽度和右边未对齐这三种标准的平面文件格式外，还提供了第四个选项： **“固定宽度并使用行分隔符”**。 此选项表示右边未对齐格式的一种特殊情况，在这种格式下，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将添加一个虚列作为最后一个数据列。 此虚列可确保最后一列具有固定宽度。  
  
 **“固定宽度并使用行分隔符”** 选项在 **“平面文件连接管理器编辑器”**中不可用。 如果需要，可以在该编辑器中模拟此选项。 若要模拟此选项，请在 **“平面文件连接管理器编辑器”** 的 **“常规”**页上，为 **“格式”**选择 **“右边未对齐”**。 然后在该编辑器的 **“高级”** 页上，添加一个新的虚列作为最后一个数据列。  
  
 **覆盖文件中的数据**  
 指示是覆盖现有文件还是向现有文件中追加数据。  
  
 **标题**  
 键入在向文件中写入任何数据之前插入到该文件中的文本块。 使用此选项可以包括其他信息，如列标题。  
  
 **预览**  
 通过使用“数据视图”对话框预览结果。 预览最多可以显示 200 行。  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [平面文件目标编辑器（“映射”页）](../../integration-services/data-flow/flat-file-destination-editor-mappings-page.md)  
  
  