---
title: "扩展 with the Script Component 数据流 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- data flow task [Integration Services], components
- data flow [Integration Services], extending
- debugging [Integration Services], components
- code design mode [Integration Services]
- metadata [Integration Services]
- scripts [Integration Services], extending data flow
- data flow components [Integration Services], Script component
- components [Integration Services], data flow
- Script component [Integration Services], about Script component
- Script component [Integration Services]
- data flow [Integration Services], components
ms.assetid: 072bc4b8-363a-4131-87c3-240338e2fa5c
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c58a854082fcbd12333be63995e4fcdf2d55aac7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="extending-the-data-flow-with-the-script-component"></a>Extending the Data Flow with the Script Component
  脚本组件扩展的数据流功能[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]用自定义代码编写的包[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual C#，编译并在包运行时执行。 当 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包含的数据流源、转换或目标不能完全满足您的需求时，脚本组件可简化自定义数据流源、转换或目标的开发。 用预期输入和输出配置该组件后，它将为您编写所有必需的基础结构代码，这样您就可以只将注意力集中于自定义处理所需的代码。  
  
 与包含程序包和数据流中的自动生成类通过脚本组件交互**ComponentWrapper**和**BufferWrapper**项目项，是实例的<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>和<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>分别类。 这些类使连接、变量和其他包项成为类型化对象，并管理输入和输出。 脚本组件还可以使用 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 命名空间、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 类库以及自定义程序集来实现自定义功能。  
  
 脚本组件及其生成的基础结构代码可以大大简化自定义数据流组件的开发过程。 但是，若要了解脚本组件的工作原理，你可能发现很有用读取部分[开发自定义数据流组件](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)了解参与开发自定义数据流组件的步骤。  
  
 如果您创建的是计划在多个包中重用的源、转换或目标，则应考虑开发自定义组件，而不是使用脚本组件。 有关详细信息，请参阅 [开发自定义数据流组件](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="in-this-section"></a>本節內容  
 下列主题提供有关脚本组件的详细信息。  
  
 [配置脚本组件编辑器中的脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
 在中配置的属性**脚本转换编辑器**影响功能和脚本组件代码的性能。  
  
 [编码和调试脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
 你使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 开发环境以开发脚本组件中所包含的脚本。  
  
 [了解脚本组件对象模型](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 新脚本组件项目包含三个带有多个类和自动生成的属性及方法的项目项。  
  
 [使用脚本组件中的变量](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)  
 **ComponentWrapper**项目项包含的包变量的强类型化访问器属性。  
  
 [连接到脚本组件中的数据源](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)  
 **ComponentWrapper**项目项还包含连接的包中定义的强类型化访问器属性。  
  
 [在脚本组件中引发事件](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md)  
 您可以引发事件来提供问题和错误的通知。  
  
 [脚本组件中的日志记录](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md)  
 您可以向包中启用的日志提供程序记录信息。  
  
 [开发特定类型的脚本组件](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
 这些简单示例说明和演示如何使用脚本组件来开发数据流源、转换和目标。  
  
 [其他脚本组件示例](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
 这些简单示例说明和演示脚本组件的一些可能的用法。  
  
## <a name="see-also"></a>另請參閱  
 [脚本组件](../../../integration-services/data-flow/transformations/script-component.md)   
 [比较脚本任务和脚本组件](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  

