---
title: 合并转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergetrans.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- merging data [Integration Services]
- Merge transformation
- combining datasets
- datasets [Integration Services], merging
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9c785ce482a1fd631a2775b7cc224ab0f737ea6a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939418"
---
# <a name="merge-transformation"></a>合并转换
  合并转换将两个排序后的数据集合并为一个数据集。 根据每个数据集中的行的键列的值，将这些行插入到输出中。  
  
 通过将合并转换纳入数据流，可以执行下列任务：  
  
-   合并两个数据源的数据，如表和文件。  
  
-   通过嵌套合并转换来创建复杂数据集。  
  
-   更正数据中的错误后重新合并行。  
  
 合并转换与 Union All 转换类似。 在下列情况下，请使用 Union All 转换代替合并转换：  
  
-   转换输入未排序。  
  
-   合并的输出无需排序。  
  
-   转换的输入超过两个。  
  
## <a name="input-requirements"></a>输入要求  
 合并转换要求输入已排序的数据。 有关此重要要求的详细信息，请参阅 [为合并转换和合并联接转换排序数据](sort-data-for-the-merge-and-merge-join-transformations.md)。  
  
 合并转换还要求输入中的已合并列具有匹配的元数据。 例如，不能合并包含数值数据类型的列和包含字符数据类型的列。 如果数据为字符串数据类型，第二个输入中列的长度必须小于或等于被合并的第一个输入中列的长度。  
  
 在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中，合并转换的用户界面会自动映射具有相同元数据的列。 然后，您可以手动映射具有兼容数据类型的其他列。  
  
 此转换有两个输入和一个输出。 它不支持错误输出。  
  
## <a name="configuration-of-the-merge-transformation"></a>合并转换的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“合并转换编辑器”** 对话框中设置的属性的详细信息，请参阅 [Merge Transformation Editor](../../merge-transformation-editor.md)。  
  
 有关可以用编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何设置属性的详细信息，请参阅以下主题：  
  
-   [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)  
  
-   [为合并转换和合并联接转换排序数据](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="see-also"></a>另请参阅  
 [合并联接转换](merge-join-transformation.md)   
 [Union All 转换](union-all-transformation.md)   
 [数据流](../data-flow.md)   
 [Integration Services 转换](integration-services-transformations.md)  
  
  
