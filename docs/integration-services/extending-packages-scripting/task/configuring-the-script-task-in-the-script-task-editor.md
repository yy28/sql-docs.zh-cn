---
title: "配置脚本任务对脚本任务编辑器 |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 182a7b8f04c2339a8f3d3b986c978a7998c8a9c3
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>在脚本任务编辑器中配置脚本任务
  在脚本任务中编写自定义代码之前，你的三个页中配置其主体属性**脚本任务编辑器**。 使用“属性”窗口可以配置非脚本任务特有的其他任务属性。  
  
> [!NOTE]  
>  在早期版本中，您可以指示是否对脚本进行预编译，而从 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 开始，不同的是，所有脚本都要预编译。  
  
## <a name="general-page-of-the-script-task-editor"></a>脚本任务编辑器的“常规”页  
 上**常规**页**脚本任务编辑器**，分配一个唯一的名称和描述脚本任务。  
  
## <a name="script-page-of-the-script-task-editor"></a>脚本任务编辑器的“脚本”页  
 **脚本**页**脚本任务编辑器**显示脚本任务的自定义属性。  
  
### <a name="scriptlanguage-property"></a>ScriptLanguage 属性  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 支持[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual C# 编程语言。 脚本任务中创建一个脚本后，你无法更改值**ScriptLanguage**属性。  
  
 若要设置的脚本任务和脚本组件的默认脚本语言，使用**ScriptLanguage**属性**常规**页**选项**对话框。 有关详细信息，请参阅 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)。  
  
### <a name="entrypoint-property"></a>EntryPoint 属性  
 **入口点**属性上指定的方法**ScriptMain**类在 VSTA 项目[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]运行时作为脚本任务代码入口点调用。 **ScriptMain**类是由脚本模板生成的默认类。  
  
 若要更改 VSTA 项目中方法的名称，则必须更改 **EntryPoint** 属性的值。  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables 和 ReadWriteVariables 属性  
 可以输入以逗号分隔的现有变量列表作为这些属性的值，使这些变量在脚本任务代码中可用于只读或读/写访问。 这两种类型的两个变量访问在代码中通过<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>属性**Dts**对象。 有关详细信息，请参阅 [Using Variables in the Script Task](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)。  
  
> [!NOTE]  
>  变量名称区分大小写。  
  
 若要选择变量，单击省略号 (**...**) 属性字段旁边的按钮。 有关详细信息，请参阅[选择变量页](../../../integration-services/control-flow/select-variables-page.md)。  
  
### <a name="edit-script-button"></a>“编辑脚本”按钮  
 **编辑脚本**按钮会启动在其中编写自定义脚本的 VSTA 开发环境。 有关详细信息，请参阅[编码和调试脚本任务](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)。  
  
## <a name="expressions-page-of-the-script-task-editor"></a>脚本任务编辑器的“表达式”页  
 上**表达式**页**脚本任务编辑器**，您可以使用表达式来为脚本任务上面列出的属性以及许多其他任务属性提供值。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [编码和调试脚本任务](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  

