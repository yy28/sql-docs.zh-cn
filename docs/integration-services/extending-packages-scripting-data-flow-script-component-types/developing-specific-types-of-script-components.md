---
title: "开发特定类型的脚本组件 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-data-flow-script-component-types
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: dfbbe959-6b4e-4b47-b9dd-bcc31929482d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5aee90e58d7a08ae8efff32a2d1020e41ee9db9d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="developing-specific-types-of-script-components"></a>开发特定类型的脚本组件
  脚本组件是一个可配置的工具，您可以在包的数据流中使用，它可以满足几乎所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 附带的源、转换和目标所无法满足的要求。 本节包含一些脚本组件代码示例，这些示例演示了用于配置脚本组件的四个选项：  
  
-   作为源。  
  
-   作为具有同步输出的转换。  
  
-   作为具有异步输出的转换。  
  
-   作为目标。  
  
 有关脚本组件的其他示例，请参阅[其他脚本组件示例](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [使用脚本组件创建源](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)  
 说明并演示如何使用脚本组件创建数据流源。  
  
 [使用脚本组件创建同步转换](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 说明并演示如何使用脚本组件创建具有同步输出的数据流转换。 这种类型的转换可在数据通过组件时原地修改数据行。  
  
 [使用脚本组件创建异步转换](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 说明并演示如何使用脚本组件创建具有异步输出的数据流转换。 这种类型的转换必须先读取所有数据行，然后才能向通过组件的数据添加更多信息，如计算聚合。  
  
 [使用脚本组件创建目标](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
 说明并演示如何使用脚本组件创建数据流目标。  
  
## <a name="see-also"></a>另请参阅  
 [比较脚本解决方案与自定义对象](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [开发特定类型的数据流组件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
  
  
