---
title: 导入列转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.importcolumntrans.f1
helpviewer_keywords:
- Import Column transformation [Integration Services]
- columns [Integration Services], importing
- importing data, SSIS packages
- inserting data
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8fd13e0b2a62e7b1bc0579a7fa5ac0de055e7243
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430394"
---
# <a name="import-column-transformation"></a>导入列转换
  导入列转换从文件中读取数据并将数据添加到数据流中的列中。 通过此转换，包可将存储于各个单独文件中的文本和图像添加到数据流中。 例如，如果某个数据流将数据加载到存储产品信息的表中，则它可包含导入列转换以便从文件中导入每个产品的客户评论并将评论添加到数据流中。  
  
 可以按照下列方式配置导入列转换：  
  
-   指定转换要向其添加数据的列。  
  
-   指定转换是否需要字节顺序标记 (BOM)。  
  
    > [!NOTE]  
    >  仅当数据为 DT_NTEXT 数据类型时才需要 BOM。  
  
 转换输入中的列包含存储数据的文件的名称。 数据集中的每一行均可指定一个不同的文件。 导入列转换处理行时，将读取文件名，打开文件系统中的相应文件，并将文件内容加载到输出列中。 输出列的数据类型必须是 DT_TEXT、DT_NTEXT 或 DT_IMAGE。 有关详细信息，请参阅 [Integration Services 数据类型](../integration-services-data-types.md)。  
  
 此转换有一个输入、一个输出和一个错误输出。  
  
## <a name="configuration-of-the-import-column-transformation"></a>导入列转换的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](../../common-properties.md)  
  
-   [转换自定义属性](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何设置数据流组件属性的信息，请参阅 [设置数据流组件属性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另请参阅  
 [导出列转换](export-column-transformation.md)   
 [数据流](../data-flow.md)   
 [Integration Services 转换](integration-services-transformations.md)  
  
  
