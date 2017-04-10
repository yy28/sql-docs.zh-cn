---
title: "平面文件目标 | Microsoft Docs"
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
  - "sql13.dts.designer.flatfiledest.f1"
helpviewer_keywords: 
  - "平面文件"
  - "平面文件目标"
  - "文本文件写入 [Integration Services]"
  - "目标 [Integration Services], 平面文件"
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
caps.latest.revision: 49
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 49
---
# 平面文件目标
  平面文件目标将数据写入文本文件。 文本文件可以为带分隔符格式、固定宽度格式、固定宽度并使用行分隔符格式或右边未对齐格式。  
  
 可以按照下列方式配置平面文件目标：  
  
-   提供在写入任何数据之前插入到文件的文本块。 该文本可以提供列标题之类信息。  
  
-   指定是否覆盖同名目标文件中的数据。  
  
 此目标用平面文件连接管理器访问文本文件。 通过设置平面文件目标所用平面文件连接管理器的属性，可以指定平面文件目标如何格式化和写入文本文件。 配置平面文件连接管理器时，请指定有关文件以及文件中每一列的信息。 例如，指定在文件中分隔列和行的字符，而且指定每列的数据类型和长度。 有关详细信息，请参阅 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
 平面文件目标包括 Header 自定义属性。 加载包时，可以通过属性表达式更新此属性。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../integration-services/expressions/integration-services-ssis-expressions.md)、[在包中使用属性表达式](../../integration-services/expressions/use-property-expressions-in-packages.md)和[平面文件自定义属性](../../integration-services/data-flow/flat-file-custom-properties.md)。  
  
 此目标具有一个输出。 它不支持错误输出。  
  
## 配置平面文件目标  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 **“平面文件源编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [平面文件目标编辑器（“连接管理器”页）](../../integration-services/data-flow/flat-file-destination-editor-connection-manager-page.md)  
  
-   [平面文件目标编辑器（“映射”页）](../../integration-services/data-flow/flat-file-destination-editor-mappings-page.md)  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../Topic/Common%20Properties.md)  
  
-   [平面文件自定义属性](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## 相关任务  
 有关如何设置数据流组件属性的信息，请参阅[设置数据流组件属性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## 另请参阅  
 [平面文件源](../../integration-services/data-flow/flat-file-source.md)   
 [数据流](../../integration-services/data-flow/data-flow.md)  
  
  