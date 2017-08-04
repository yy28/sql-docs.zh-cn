---
title: "平面文件自定义属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 097c9a07d738bb1b192095ac91448487fdfa0eb1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="flat-file-custom-properties"></a>平面文件自定义属性
  **源自定义属性**  
  
 平面文件源具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍平面文件源的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|字符串|包含文件名的输出列的名称。 如果未指定名称，则不会生成包含文件名的输出列。<br /><br /> 注意：此属性未在 **平面文件源编辑器**中提供，但可以使用 **高级编辑器**进行设置。|  
|RetainNulls|Boolean|该值指定当数据转换管道引擎处理数据时是否将源文件中的 Null 值仍保留为 Null 值。 此属性的默认值为 **False**。|  
  
 平面文件源的输出没有自定义属性。  
  
 下表描述了平面文件源的输出列的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|FastParse|Boolean|一个值，该值指示列是使用 DTS 提供的不区分区域设置的较快分析例程，还是使用标准的区分区域设置的分析例程。 有关详细信息，请参阅 [Fast Parse](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) 和 [Standard Parse](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)。 此属性的默认值为 **False**。<br /><br /> 注意：此属性未在 **平面文件源编辑器**中提供，但可以使用 **高级编辑器**进行设置。|  
  
 有关详细信息，请参阅 [Flat File Source](../../integration-services/data-flow/flat-file-source.md)。  
  
 **目标自定义属性**  
  
 平面文件目标具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍平面文件目标的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|标题|字符串|写入任何数据之前插入到文件中的文本块。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
|Overwrite|Boolean|一个值，指定是覆盖还是追加到具有相同名称的现有目标文件。 此属性的默认值为 **True**。|  
  
 平面文件目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [Flat File Destination](../../integration-services/data-flow/flat-file-destination.md)。  
  
## <a name="see-also"></a>另请参阅  
 [通用属性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
