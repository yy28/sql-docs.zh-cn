---
title: "XML 源编辑器（“连接管理器”页） | Microsoft Docs"
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
  - "sql13.dts.designer.xmlsourceadapter.connectionmanager.f1"
helpviewer_keywords: 
  - "“XML 源编辑器”"
ms.assetid: e6507403-a3ce-4b6f-91fc-a7de9f7b6283
caps.latest.revision: 20
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 20
---
# XML 源编辑器（“连接管理器”页）
  可以使用 **“XML 源编辑器”** 的 **“连接管理器”** 页指定 XML 文件和转换 XML 数据的 XSD。  
  
 有关 XML 源的详细信息，请参阅 [XML Source](../../integration-services/data-flow/xml-source.md)。  
  
## 静态选项  
 **数据访问模式**  
 指定从源选择数据的方法。  
  
|“值”|Description|  
|-----------|-----------------|  
|XML 文件位置|从 XML 文件检索数据。|  
|来自变量的 XML 文件|在变量中指定 XML 文件名。<br /><br /> **相关信息：** [在包中使用变量](../Topic/Use%20Variables%20in%20Packages.md)|  
|来自变量的 XML 数据|从变量检索 XML 数据。|  
  
 **使用内联架构**  
 指定 XML 源数据本身是否包含 XSD 架构（用于定义和验证 XML 源数据的结构和数据）。  
  
 **XSD 位置**  
 键入 XSD 架构文件的路径和文件名，或者可以单击“浏览”定位该文件。  
  
 **浏览**  
 使用“打开”对话框定位到 XSD 架构文件。  
  
 **生成 XSD**  
 使用“另存为”对话框可以为自动生成的 XSD 架构文件选择位置。 编辑器将根据 XML 数据的结构来推断架构。  
  
## 数据访问模式动态选项  
  
### 数据访问模式 = XML 文件位置  
 **XML 位置**  
 键入 XML 数据文件的路径和文件名，或者通过单击“浏览”查找文件。  
  
 **浏览**  
 使用“打开”对话框定位到 XML 数据文件。  
  
### 数据访问模式 = 来自变量的 XML 文件  
 **变量名称**  
 选择包含 XML 文件的路径和文件名的变量。  
  
### 数据访问模式 = 来自变量的 XML 数据  
 **变量名称**  
 选择包含 XML 数据的变量。  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [XML 源编辑器（“列”页）](../../integration-services/data-flow/xml-source-editor-columns-page.md)   
 [XML 源编辑器（“错误输出”页）](../../integration-services/data-flow/xml-source-editor-error-output-page.md)   
 [使用 XML 源提取数据](../../integration-services/data-flow/extract-data-by-using-the-xml-source.md)  
  
  