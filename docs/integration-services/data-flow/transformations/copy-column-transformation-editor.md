---
title: "复制列转换编辑器 | Microsoft Docs"
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
  - "sql13.dts.designer.copymaptransformation.f1"
helpviewer_keywords: 
  - "复制列转换编辑器"
ms.assetid: d8e70541-d563-4ce4-bf66-bc888a0d3026
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# 复制列转换编辑器
  可以使用 **“复制列转换编辑器”** 对话框选择要复制的列，以及为新的输出列指定名称。  
  
 若要了解有关复制列转换的详细信息，请参阅 [Copy Column Transformation](../../../integration-services/data-flow/transformations/copy-column-transformation.md)。  
  
> [!NOTE]  
>  如果只是将所有源数据复制到目标，可能无需使用复制列转换。 某些情况下，如果不需要进行任何数据转换，可以直接将源连接到目标。 在这些情况下，使用 SQL Server 导入和导出向导创建包通常更可取。 以后，您可以根据需要增强并重新配置包。 有关更多信息，请参见 [SQL Server Import and Export Wizard](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md)。  
  
## 选项  
 **可用输入列**  
 使用复选框选择要复制的列。 选择后，会将输入列添加到下表中。  
  
 **输入列**  
 从可用的输入列列表中选择要复制的列。 通过选中 **“可用输入列”** 表中的复选框来选择列。  
  
 **输出别名**  
 为每个新的输出列键入一个别名。 默认值为输入列名称后面跟着 **“的副本”**；不过，您也可以任选一个唯一的描述性名称。  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  