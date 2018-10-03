---
title: 开发特定类型的脚本组件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: dfbbe959-6b4e-4b47-b9dd-bcc31929482d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c5e2ff22d792e8c71b4d485091b7cff3a71fb6dc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193447"
---
# <a name="developing-specific-types-of-script-components"></a>开发特定类型的脚本组件
  脚本组件是一个可配置的工具，您可以在包的数据流中使用，它可以满足几乎所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 附带的源、转换和目标所无法满足的要求。 本节包含一些脚本组件代码示例，这些示例演示了用于配置脚本组件的四个选项：  
  
-   作为源。  
  
-   作为具有同步输出的转换。  
  
-   作为具有异步输出的转换。  
  
-   作为目标。  
  
 有关脚本组件的其他示例，请参阅[其他脚本组件示例](../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [使用脚本组件创建源](creating-a-source-with-the-script-component.md)  
 说明并演示如何使用脚本组件创建数据流源。  
  
 [使用脚本组件创建同步转换](creating-a-synchronous-transformation-with-the-script-component.md)  
 说明并演示如何使用脚本组件创建具有同步输出的数据流转换。 这种类型的转换可在数据通过组件时原地修改数据行。  
  
 [使用脚本组件创建异步转换](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 说明并演示如何使用脚本组件创建具有异步输出的数据流转换。 这种类型的转换必须先读取所有数据行，然后才能向通过组件的数据添加更多信息，如计算聚合。  
  
 [使用脚本组件创建目标](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
 说明并演示如何使用脚本组件创建数据流目标。  
  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services** <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [比较脚本解决方案与自定义对象](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [开发特定类型的数据流组件](../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
  
  
