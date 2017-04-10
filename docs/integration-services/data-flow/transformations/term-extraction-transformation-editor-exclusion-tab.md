---
title: "字词提取转换编辑器（“排除”选项卡） | Microsoft Docs"
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
  - "sql13.dts.designer.termextraction.inclusionexclusion.f1"
helpviewer_keywords: 
  - "字词提取转换编辑器"
ms.assetid: 90110d95-fd97-4542-9cda-832c86606130
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# 字词提取转换编辑器（“排除”选项卡）
  可以使用 **“字词提取转换编辑器”** 对话框的 **“排除”** 选项卡，建立与排除表的连接并指定包含排除字词的列。  
  
 若要了解有关字词提取转换的详细信息，请参阅 [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)。  
  
## 选项  
 **使用排除字词**  
 指示在字词提取过程中是否通过指定包含排除字词的列来排除特定的字词。 如果选择要排除字词，则必须指定以下源属性：  
  
 **OLE DB 连接管理器**  
 选择现有的 OLE DB 连接管理器，或通过单击“新建”创建新的连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”对话框创建与数据库的新连接。  
  
 **表或视图**  
 选择包含排除字词的表或视图。  
  
 **列**  
 在表或视图中选择包含排除字词的列。  
  
 **配置错误输出**  
 使用“配置错误输出”[](../Topic/Configure%20Error%20Output.md)对话框可以为导致错误的行指定错误处理方式。  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)   
 [字词提取转换编辑器（“字词提取”选项卡）](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-term-extraction-tab.md)   
 [字词提取转换编辑器（“高级”选项卡）](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-advanced-tab.md)   
 [字词查找转换](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
  