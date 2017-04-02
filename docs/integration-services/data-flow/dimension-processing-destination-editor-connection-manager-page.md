---
title: "维度处理目标编辑器（“连接管理器”页） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dimprocessingtransformation.connection.f1"
helpviewer_keywords: 
  - "维度处理目标编辑器"
ms.assetid: 44aab631-d62d-4895-8fc7-7f1f3b1b68ce
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# 维度处理目标编辑器（“连接管理器”页）
  可以使用 **“维度处理目标编辑器”** 对话框的 **“连接管理器”** 页指定与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例之间的连接。  
  
 若要了解有关维度处理目标的详细信息，请参阅 [Dimension Processing Destination](../../integration-services/data-flow/dimension-processing-destination.md)。  
  
## 选项  
 **“ODBC 目标编辑器”**  
 从列表中选择现有连接管理器，或单击“新建”创建新的连接管理器。  
  
 **新建**  
 通过使用“添加 Analysis Services 连接管理器”对话框创建一个新连接。  
  
 **可用维度列表**  
 选择要处理的维度。  
  
 **处理方法**  
 选择要应用于列表中选定维度的处理方法。 此选项的默认值为 **“完全”**。  
  
|“值”|Description|  
|-----------|-----------------|  
|**添加(增量式)**|对维度执行增量处理。|  
|**Full**|对维度执行完全处理。|  
|**Update**|对维度执行更新处理。|  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [维度处理目标编辑器（“映射”页）](../../integration-services/data-flow/dimension-processing-destination-editor-mappings-page.md)   
 [维度处理目标编辑器（“高级”页）](../../integration-services/data-flow/dimension-processing-destination-editor-advanced-page.md)  
  
  