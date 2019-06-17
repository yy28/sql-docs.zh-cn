---
title: 复制列转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.copycolumntrans.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7ebdcc68c4fe8c4782251e2f4e5896e4557e23e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770323"
---
# <a name="copy-column-transformation"></a>复制列转换
  复制列转换通过复制输入列并将新列添加到转换输出来创建新列。 以后在数据流中，可将不同的转换应用到列副本。 例如，您可以使用复制列转换来创建列的副本，然后使用字符映射表转换将复制的数据转换为大写字符，或使用聚合转换将聚合应用到此新列。  
  
## <a name="configuration-of-the-copy-column-transformation"></a>复制列转换的配置  
 可以通过指定要复制的输入列来配置复制列转换。 可以在一个操作中创建一列的多个副本，或创建多个列的副本。  
  
 此转换有一个输入和一个输出。 它不支持错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“复制列转换编辑器”** 对话框中设置的属性的详细信息，请参阅 [Copy Column Transformation Editor](../../copy-column-transformation-editor.md)。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [转换自定义属性](transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据流](../data-flow.md)   
 [Integration Services 转换](integration-services-transformations.md)  
  
  
