---
title: 设置用户定义变量的属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- modifying variables
- variables [Integration Services], properties
ms.assetid: f98ddbec-f668-4dba-a768-44ac3ae0536f
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9cd85ac29d34f40e9473f28444c8b727543d6ecf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075587"
---
# <a name="set-the-properties-of-a-user-defined-variable"></a>设置用户定义变量的属性
  若要在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中设置用户定义的变量的属性，可以使用下列功能之一：  
  
-   “变量”窗口。  
  
-   属性窗口。 “属性”窗口中列出了用于配置“变量”窗口中不可用变量的属性：Description、EvaluateAsExpression、Expression、ReadOnly、ValueType 和 IncludeInDebugDump。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 还提供了一组无法更新属性的系统变量，但 RaiseChangedEvent 属性例外。  
  
 **对变量设置表达式**  
  
 使用“属性”窗口对用户定义变量设置表达式时：  
  
-   可通过 Value 属性或 Expression 属性来设置变量的值。 默认情况下，EvaluateAsExpression 属性设置为`False`和变量的值通过值属性设置。 若要使用表达式设置的值，您必须首先将 EvaluateAsExpression 设置为`True`，然后提供表达式属性中的表达式。 Value 属性自动设置为该表达式的计算结果。  
  
-   ValueType 属性包含 Value 属性中的值的数据类型。 通过表达式设置 Value 时，ValueType 将自动更新为与该表达式的计算结果兼容的数据类型。 例如，如果 Value 包含 0,valuetype ValueType 属性包含**Int32** ，然后将表达式设置为 getdate （）、 值包含当前日期和时间和 ValueType 会设置为`DateTime`。  
  
-   通过变量的 **“属性”** 窗口，可以访问 **“表达式生成器”** 对话框。 使用该工具可以生成、验证和计算表达式。 有关详细信息，请参阅[表达式生成器](expressions/expression-builder.md)和 [Integration Services (SSIS) 表达式](expressions/integration-services-ssis-expressions.md)。  
  
 使用“变量”窗口对用户定义变量设置表达式时：  
  
-   若要使用表达式来设置变量值，首先请确认变量数据类型与表达式的计算结果兼容，然后提供中的表达式`Expression`的列**变量**窗口。 中的 EvaluateAsExpression 属性**属性**窗口将自动设置为`True`。  
  
-   如果为变量指定了表达式，则该变量旁边将显示一个特殊图标标记。 这个特殊的图标标记还显示在设置有表达式的连接管理器和任务旁边。  
  
-   通过变量的 **“变量”** 窗口，可以访问 **“表达式生成器”** 对话框。 使用该工具可以生成、验证和计算表达式。 有关详细信息，请参阅[表达式生成器](expressions/expression-builder.md)和 [Integration Services (SSIS) 表达式](expressions/integration-services-ssis-expressions.md)。  
  
 在这种**变量**并**属性**窗口中，如果将表达式分配给变量，并`EvaluateAsExpression`设置为`True`，无法更改变量数据类型。  
  
 **设置 Namespace 和 Name 属性**  
  
 值`Name`和`Namespace`属性必须以字母字符开头，如 Unicode 标准 2.0 中或下划线 (_) 所定义。 后续字符可以是在 Unicode 标准 2.0 中定义的字母或数字，或是下划线 (\_)。  
  
## <a name="using-the-variables-window-to-set-properties"></a>使用变量窗口设置属性  
  
#### <a name="to-set-the-properties-of-a-variable-by-using-the-variables-window"></a>使用变量窗口设置变量的属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，右键单击该包将其打开。  
  
3.  在 **SSIS** 菜单上单击 **“变量”**。  
  
     您可以通过将 View.Variables 命令映射到在 **“选项”** 对话框的 **“键盘”** 页上选择的组合键来显示 **“变量”** 窗口。  
  
4.  或者，在 **“变量”** 窗口中单击 **“网格选项”**，然后选择要出现在 **“变量”** 窗口中的列，并选择要应用到变量列表的筛选器。  
  
5.  在列表中，选择该变量，然后更新中的值`Name`，**数据类型**， `Value`， `Namespace`，**引发更改事件**，**说明、** 和`Expression`列。  
  
6.  在列表中选择变量，然后单击 **“移动变量”** 以更改作用域。  
  
7.  若要保存已更新的包，请在 **“文件”** 菜单中单击 **“保存选定项”**。  
  
## <a name="using-the-properties-window-to-set-properties"></a>使用属性窗口设置属性  
  
#### <a name="to-set-the-properties-of-a-variable-by-using-the-properties-window"></a>使用属性窗口设置变量的属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，右键单击该包将其打开。  
  
3.  在 **“视图”** 菜单上，单击 **“属性窗口”**。  
  
4.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，单击 **“包资源管理器”** 选项卡，并展开“包”节点。  
  
5.  若要修改包范围内的变量，请展开“变量”节点，如果看不到该节点，请展开“事件处理程序”或“可执行文件”节点，直到找到包含要修改的变量的“变量”节点。  
  
6.  单击要修改其属性的变量。  
  
7.  在“属性”窗口中，更改读/写变量属性。 对于用户定义的变量而言，某些属性为可读/只读。  
  
     有关属性的详细信息，请参阅 [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)。  
  
8.  若要保存已更新的包，请在 **“文件”** 菜单中单击 **“保存选定项”**。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)   
 [在包中使用变量](../../2014/integration-services/use-variables-in-packages.md)   
 [添加、删除、更改包中用户定义变量的作用域](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
  
