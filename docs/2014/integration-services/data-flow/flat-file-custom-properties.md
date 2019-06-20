---
title: 平面文件自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0a0516d2e038f206c140f010c2ca4a459f79956a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62902044"
---
# <a name="flat-file-custom-properties"></a>平面文件自定义属性
  **源自定义属性**  
  
 平面文件源具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍平面文件源的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|String|包含文件名的输出列的名称。 如果未指定名称，则不会生成包含文件名的输出列。<br /><br /> 注意：此属性未在平面文件源编辑器中提供，但可以使用“高级编辑器”进行设置。|  
|RetainNulls|Boolean|该值指定当数据转换管道引擎处理数据时是否将源文件中的 Null 值仍保留为 Null 值。 此属性的默认值为 `False`。|  
  
 平面文件源的输出没有自定义属性。  
  
 下表描述了平面文件源的输出列的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|FastParse|Boolean|一个值，该值指示列是使用 DTS 提供的不区分区域设置的较快分析例程，还是使用标准的区分区域设置的分析例程。 有关详细信息，请参阅 [Fast Parse](../fast-parse.md) 和 [Standard Parse](../standard-parse.md)。 此属性的默认值为 `False`。<br /><br /> 注意：此属性未在平面文件源编辑器中提供，但可以使用“高级编辑器”进行设置。|  
  
 有关详细信息，请参阅 [Flat File Source](flat-file-source.md)。  
  
 **目标自定义属性**  
  
 平面文件目标具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍平面文件目标的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|Header|String|写入任何数据之前插入到文件中的文本块。<br /><br /> 此属性的值可以使用属性表达式来指定。|  
|Overwrite|Boolean|一个值，指定是覆盖还是追加到具有相同名称的现有目标文件。 此属性的默认值为 `True`。|  
  
 平面文件目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [Flat File Destination](flat-file-destination.md)。  
  
## <a name="see-also"></a>请参阅  
 [Common Properties](../common-properties.md)  
  
  
