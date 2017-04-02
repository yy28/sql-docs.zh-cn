---
title: "合并联接转换 | Microsoft Docs"
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
  - "sql13.dts.designer.mergejointrans.f1"
helpviewer_keywords: 
  - "数据集 [Integration Services]"
  - "合并联接转换"
  - "数据集 [Integration Services], 联接"
  - "联接数据集 [Integration Services]"
  - "联接 [SQL Server], SSIS"
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
caps.latest.revision: 54
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 54
---
# 合并联接转换
  合并联接转换提供了一个输出，该输出是通过使用 FULL、LEFT 或 INNER 联接将两个已排序数据集进行联接而生成的。 例如，可使用 LEFT 联接来联接包含产品信息的表与列出产品的制造国家/地区的表。 结果是一个列出所有产品及其产地国家/地区的表。  
  
 可以按照下列方法来配置合并联接转换：  
  
-   指定联接是 FULL、LEFT 联接，还是 INNER 联接。  
  
-   指定联接所使用的列。  
  
-   指定转换是否将空值处理为等于其他空值。  
  
    > [!NOTE]  
    >  如果不将空值处理为相等的值，则转换将如同 SQL Server 数据库引擎那样处理空值。  
  
 此转换有两个输入和一个输出。 它不支持错误输出。  
  
## 输入要求  
 合并联接转换要求输入已排序的数据。 有关此重要要求的详细信息，请参阅[为合并转换和合并联接转换排序数据](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
## 联接要求  
 合并联接转换要求被联接的列具有匹配的元数据。 例如，不能将具有数值数据类型的列和具有字符数据类型的列相联接。 如果数据为字符串数据类型，第二个输入中列的长度必须小于或等于被合并的第一个输入中列的长度。  
  
## 缓冲区中止  
 您不再必须配置 **MaxBuffersPerInput** 属性的值，因为 Microsoft 已进行了更改，减少了合并联接转换将占用过多内存的风险。 在合并联接的多个输入以不相等速率生成数据时，有时候可能会发生此问题。  
  
## 相关任务  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关如何设置此转换的属性的信息，请单击下列主题之一：  
  
-   [使用合并联接转换扩展数据集](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)  
  
-   [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [为合并转换和合并联接转换排序数据](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## 另请参阅  
 [合并联接转换编辑器](../../../integration-services/data-flow/transformations/merge-join-transformation-editor.md)   
 [合并转换](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Union All 转换](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Integration Services 转换](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  