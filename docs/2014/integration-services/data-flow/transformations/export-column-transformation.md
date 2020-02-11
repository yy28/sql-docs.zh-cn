---
title: 导出列转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exportcolumntrans.f1
helpviewer_keywords:
- exporting data
- append options [Integration Services]
- Export Column transformation [Integration Services]
- columns [Integration Services], exporting
- inserting data
- truncate options [Integration Services]
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ecb72ee0cb9d6e94a672f46ed523096ac4cc096e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62900153"
---
# <a name="export-column-transformation"></a>导出列转换
  导出列转换读取数据流中的数据，并将数据插入到文件中。 例如，如果数据流包含产品信息（如每件产品的图片），则可使用导出列转换将图像保存到文件中。  
  
## <a name="append-and-truncate-options"></a>追加和截断选项  
 下表说明了追加和截断选项的设置如何影响结果。  
  
|附加|Truncate|文件存在|结果|  
|------------|--------------|-----------------|-------------|  
|False|False|否|该转换将创建一个新文件并将数据写入到该文件中。|  
|True|False|否|该转换将创建一个新文件并将数据写入到该文件中。|  
|False|True|否|该转换将创建一个新文件并将数据写入到该文件中。|  
|True|True|否|该转换的设计时验证失败。 将两个属性都设置为 `true` 是无效的。|  
|False|False|是|发生运行时错误。 文件存在，但转换无法写入到文件中。|  
|False|True|是|转换将删除文件，然后重新创建文件并将数据写入到文件中。|  
|True|False|是|转换将打开文件并将数据写入到文件末尾。|  
|True|True|是|该转换的设计时验证失败。 将两个属性都设置为 `true` 是无效的。|  
  
## <a name="configuration-of-the-export-column-transformation"></a>导出列转换的配置  
 可以按照下列方式配置导出列转换：  
  
-   指定数据列和包含要向其写入数据的文件的路径的列。  
  
-   指定数据插入操作是追加还是截断现有文件。  
  
-   指定是否将字节顺序标记 (BOM) 写入到文件中。  
  
    > [!NOTE]  
    >  仅在不将数据追加到现有文件且数据具有 DT_NTEXT 数据类型时写入 BOM。  
  
 此转换使用成对的输入列：一列包含文件名，另一列包含数据。 数据集中的每一行都可指定一个不同的文件。 转换在处理行时，数据将插入到指定的文件中。 在运行时，如果这些文件不存在，转换将创建这些文件，然后将数据写入到文件中。 要写入的数据必须具有 DT_TEXT、DT_NTEXT 或 DT_IMAGE 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../integration-services-data-types.md)。  
  
 此转换有一个输入、一个输出和一个错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在“导出列转换编辑器”**** 对话框中设置的属性的详细信息，请参阅[导出列转换编辑器（“列”页）](../../export-column-transformation-editor-columns-page.md)。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](../../common-properties.md)  
  
-   [转换自定义属性](transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)。  
  
  
