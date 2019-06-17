---
title: 脚本任务编辑器 （脚本页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scripttask.script.f1
helpviewer_keywords:
- Script Task Editor
ms.assetid: 93da0e0d-83f5-406d-b144-4cce216571cb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 037b176dfacd9420fba64a405d8c851c558e93e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056191"
---
# <a name="script-task-editor-script-page"></a>脚本任务编辑器（“脚本”页）
  使用 **“脚本任务编辑器”** 对话框的 **“脚本”** 页，可以设置脚本属性并指定脚本可以访问的变量。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssISversion10](../includes/ssisversion10-md.md)] 和更高版本中，所有脚本都将预编译。 而在早期版本中，要设置 **PrecompileScriptIntoBinaryCode** 属性来指定是否对脚本进行预编译。  
  
 若要了解有关脚本任务的详细信息，请参阅 [Script Task](control-flow/script-task.md) 和 [在脚本任务编辑器中配置脚本任务](extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)。 若要了解如何对脚本任务进行编程，请参阅 [Extending the Package with the Script Task](extending-packages-scripting/task/extending-the-package-with-the-script-task.md)。  
  
## <a name="options"></a>选项  
 **ScriptLanguage**  
 选择任务的脚本语言， [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#。  
  
 创建任务的脚本后，将无法更改 **ScriptLanguage** 属性的值。  
  
 若要设置脚本任务的默认脚本语言，请使用 **“选项”** 对话框的 **“常规”** 页上的 **“脚本语言”** 选项。 有关详细信息，请参阅 [General Page](general-page-of-integration-services-designers-options.md)。  
  
 **EntryPoint**  
 指定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 运行时作为脚本任务代码入口点调用的方法。 指定的方法必须在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA) 的 ScriptMain 类中。ScriptMain 类是脚本模板生成的默认类。  
  
 若要更改 VSTA 项目中方法的名称，则必须更改 **EntryPoint** 属性的值。  
  
 **ReadOnlyVariables**  
 以逗号分隔的形式键入一列可供脚本使用的只读变量，或单击省略号 (…) 按钮，然后在“选择变量”对话框中选择变量   。  
  
> [!NOTE]  
>  变量名称区分大小写。  
  
 **ReadWriteVariables**  
 以逗号分隔的形式键入一列可供脚本使用的读/写变量，或单击省略号 (…) 按钮，然后在“选择变量”对话框中选择变量   。  
  
> [!NOTE]  
>  变量名称区分大小写。  
  
 **编辑脚本**  
 打开 VSTA IDE，您可以在其中创建或修改脚本。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [General Page](general-page-of-integration-services-designers-options.md)   
 [脚本任务编辑器（“常规”页）](../../2014/integration-services/script-task-editor-general-page.md)   
 [“表达式”页](expressions/expressions-page.md)   
 [脚本任务示例](extending-packages-scripting-task-examples/script-task-examples.md)   
 [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)   
 [添加、删除、更改包中用户定义变量的作用域](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
  
