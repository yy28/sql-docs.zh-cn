---
title: 行计数转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.rowcounttrans.f1
helpviewer_keywords:
- updating variables
- Row Count transformation
- number of rows
- variables [Integration Services], updating
- counting rows
ms.assetid: b68293b9-a68c-40be-9d81-77342da1be29
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 035ba7e1777dac88efb59265ea61ab6181bada1f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027951"
---
# <a name="row-count-transformation"></a>行计数转换
  行计数转换在行通过数据流时对行进行计数，并将最终计数结果存储在一个变量中。  
  
 A [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包可使用行计数来更新脚本、表达式和属性表达式中使用的变量。 （例如，存储行计数的变量可更新电子邮件中的消息正文，以便包含行数。）行计数转换使用的变量必须已经存在，并且必须在带有行计数转换的数据流所属的数据流任务作用域内。  
  
 只有在最后一行已通过转换后，转换才会在变量中存储行计数值。 因此，该变量值并不即时更新以在包含行计数转换的数据流中使用更新值。 您可以在单独的数据流中使用更新的变量。  
  
 此转换有一个输入和一个输出。 它不支持错误输出。  
  
## <a name="configuration-of-the-row-count-transformation"></a>行计数转换的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [转换自定义属性](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何设置数据流组件属性的信息，请参阅 [设置数据流组件属性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services &#40;SSIS&#41;变量](../../integration-services-ssis-variables.md)   
 [数据流](../data-flow.md)   
 [Integration Services 转换](integration-services-transformations.md)  
  
  