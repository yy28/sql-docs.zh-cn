---
title: "Union All 转换 | Microsoft Docs"
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
  - "sql13.dts.designer.unionalltrans.f1"
helpviewer_keywords: 
  - "合并数据集 [Integration Services]"
  - "组合数据集"
  - "Union All 转换"
  - "数据集 [Integration Services], 合并"
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# Union All 转换
  Union All 转换将多个输入组合到一个输出中。 例如，可将来自五个不同平面文件源的输出输入到 Union All 转换并将其组合到一个输出中。  
  
## 输入和输出  
 转换输入是一个接一个地添加到转换输出中的；不对行进行重新排序。 如果包需要排序的输出，则应使用合并转换而不是 Union All 转换。  
  
 连接到 Union All 转换的第一个输入是转换从中创建转换输出的输入。 随后连接到转换的输入中的列将会被映射到转换输出中的列。  
  
 若要合并输入，可将输入中的列映射到输出中的列。 每个输出列至少要有一个输入中的列与其映射。 两列间的映射要求各列的元数据相匹配。 例如，映射列必须具有相同的数据类型。  
  
 如果映射列包含字符串数据，并且输出列的长度比输入列短，则输出列长度会自动增加以便包含输入列。 未映射到输出列的输入列在输出列中被设置为空值。  
  
 此转换具有多个输入和一个输出。 它不支持错误输出。  
  
## Union All 转换的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“Union All 转换编辑器”** 对话框中设置的属性的详细信息，请参阅 [Union All Transformation Editor](../../../integration-services/data-flow/transformations/union-all-transformation-editor.md)。  
  
 有关可以编程方式设置的属性的详细信息，请参阅 [Common Properties](../Topic/Common%20Properties.md)。  
  
 有关如何设置属性的详细信息，请单击下列主题之一：  
  
-   [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## 相关任务  
 [通过使用 Union All 转换来合并数据](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)  
  
  