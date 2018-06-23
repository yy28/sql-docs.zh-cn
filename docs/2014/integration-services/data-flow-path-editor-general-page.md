---
title: 数据流路径编辑器 （常规页） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.patheditor.general.f1
helpviewer_keywords:
- Data Flow Path Editor dialog box
ms.assetid: 72a9ff1d-3748-41d1-a9b2-63f4a77bba24
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9ba5e08523500fa104f96a760cf57c9657e473d0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017605"
---
# <a name="data-flow-path-editor-general-page"></a>数据流路径编辑器（“常规”页）
  可以使用 **“数据流路径编辑器”** 对话框设置路径属性，查看列元数据以及管理附加到路径的数据查看器。  
  
 使用 **“数据流路径编辑器”** 对话框的 **“常规”** 节点可以对路径进行命名和说明以及指定路径批注选项。  
  
## <a name="options"></a>“常规”  
 **名称**  
 为路径提供唯一的名称。  
  
 **ID**  
 路径的沿袭标识符。 该属性为只读。  
  
 **IdentificationString**  
 用于标识路径的字符串。 从上面输入的名称自动生成。  
  
 **Description**  
 描述该路径。  
  
 **PathAnnotation**  
 指定要使用的批注类型。 选择 **Never** 可以禁用批注；选择 **AsNeeded** 可以启用按需批注；选择 **SourceName** 可以使用 **SourceName** 选项的值自动进行批注；选择 **PathName** 可以使用 **Name** 属性的值自动进行批注。  
  
 **DestinationName**  
 显示作为路径结尾的输入。  
  
 **SourceName**  
 显示作为路径开头的输出。  
  
## <a name="see-also"></a>请参阅  
 [数据流路径编辑器&#40;元数据页&#41;](../../2014/integration-services/data-flow-path-editor-metadata-page.md)   
 [数据流路径编辑器&#40;数据查看器页&#41;](../../2014/integration-services/data-flow-path-editor-data-viewers-page.md)   
 [数据流](data-flow/data-flow.md)   
 [在包中使用批注](use-annotations-in-packages.md)  
  
  