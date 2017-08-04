---
title: "使用脚本组件中的变量 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bac1e6d96e872be0355282c3e12fc81054ca41cd
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="using-variables-in-the-script-component"></a>在脚本组件中使用变量
  变量存储包及其容器、任务和事件处理程序在运行时可以使用的值。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../../integration-services/integration-services-ssis-variables.md)。  
  
 你可以使现有变量可用于只读或读/写访问由你的自定义脚本通过输入以逗号分隔列表中的变量**ReadOnlyVariables**和**ReadWriteVariables**字段上**脚本**页**脚本转换编辑器**。 请注意，变量名称区分大小写。 使用**值**属性来读取和写入到单个变量。 当脚本在运行时操作变量时，脚本组件将在后台处理任何所需的锁定。  
  
> [!IMPORTANT]  
>  集合**ReadWriteVariables**选项仅适用于**PostExecute**方法来最大化性能并降低发生锁定冲突的风险。 因此不能在处理每行数据时直接递增包变量的值， 相反，递增的值的本地变量，并将包变量的值设置为中的本地变量的值**PostExecute**方法之后的所有数据已处理。 还可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 属性解决此限制问题，本主题稍后会进行介绍。 但是，在处理每一行时直接写包变量将会对性能产生负面影响，并增加锁定冲突的风险。  
  
 有关详细信息**脚本**页**脚本转换编辑器**，请参阅[配置脚本组件编辑器中的脚本组件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)和[脚本转换编辑器 &#40;脚本页 &#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
 脚本组件创建**变量**中的集合类**ComponentWrapper**项目项的属性的值为强类型化访问器的每个预配置的变量，其中属性具有与变量本身相同的名称。 此集合公开通过**变量**属性**ScriptMain**类。 取值函数属性根据需要提供对变量值的只读或读/写权限。 例如，如果你已添加名为的整数变量`MyIntegerVariable`到**ReadOnlyVariables**列表中，你可以检索其值在脚本中使用以下代码：  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 还可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 属性（通过调用 `Me.VariableDispenser` 进行访问）在脚本组件中使用变量。 在这种情况下，使用的不是变量的已命名类型化取值函数属性，而是直接访问这些变量。 使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 时，您必须在您自己的代码中处理锁定语义和变量值的数据类型转换。 如果要使用在设计时不可用，而是以编程方式在运行时创建的变量，则必须使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 属性，而不是已命名的类型化取值函数属性。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS &#41;变量](../../../integration-services/integration-services-ssis-variables.md)   
 [在包中使用变量](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
