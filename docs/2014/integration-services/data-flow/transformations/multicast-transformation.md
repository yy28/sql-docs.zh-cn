---
title: 多播转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multicasttrans.f1
helpviewer_keywords:
- multiple outputs
- Multicast transformation
- datasets [Integration Services], multiple outputs
- multiple transformations
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a05605ca5c2b35b0a5e35c8228a2a144f20d7905
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374049"
---
# <a name="multicast-transformation"></a>多播转换
  多播转换将其输入分发到一个或多个输出。 此转换与有条件拆分转换类似。 这两种转换都将一个输入定向到多个输出。 这两者之间的区别在于多播转换将每行定向到每个输出，而有条件拆分则将一行定向到单个输出。 有关详细信息，请参阅 [Conditional Split Transformation](conditional-split-transformation.md)。  
  
 您可以通过添加输出来配置多播转换。  
  
 使用多播转换，包可创建数据的逻辑副本。 当包需要对相同的数据应用多个转换集时，此功能十分有用。 例如，对数据的一个副本进行聚合并且仅将摘要信息加载到其目标，而对数据的另一个副本使用查找值和派生列进行扩展，然后再将其加载到目标。  
  
 此转换具有一个输入和多个输出。 它不支持错误输出。  
  
## <a name="configuration-of-the-multicast-transformation"></a>多播转换的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可在 **“多播转换编辑器”** 对话框中设置的属性的详细信息，请参阅 [Multicast Transformation Editor](../../multicast-transformation-editor.md)。  
  
 有关可以编程方式设置的属性的信息，请参阅 [Common Properties](../../common-properties.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何设置数据流组件属性的信息，请参阅 [设置数据流组件属性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据流](../data-flow.md)   
 [Integration Services 转换](integration-services-transformations.md)  
  
  
