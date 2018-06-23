---
title: 比较脚本任务和脚本组件 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], comparing to Script component
- Script component [Integration Services], comparing to Script task
ms.assetid: 4b73753a-4239-491b-b7a6-abc63ba83d2d
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e16ca8fdd139117afd7863be67e1890ada546f88
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026177"
---
# <a name="comparing-the-script-task-and-the-script-component"></a>比较脚本任务和脚本组件
  脚本任务在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 设计器的“控制流”窗口中，脚本组件在“数据流”窗口中，它们在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包中的用途非常不同。 任务是一般用途的控制流工具，而组件用作数据流中的源、转换或目标。 尽管它们的用途不同，但是脚本任务和脚本组件在所使用的编码工具和在包中供开发人员使用的对象方面还是有一些相似之处的。 了解它们的相似与不同之处有助于您更有效地使用任务和组件。  
  
## <a name="similarities-between-the-script-task-and-the-script-component"></a>脚本任务和脚本组件之间的相似之处  
 脚本任务和脚本组件有以下相同特性。  
  
|功能|Description|  
|-------------|-----------------|  
|两个设计时模式|在任务和组件中，都是从在编辑器中指定属性开始，然后切换到开发环境编写代码。|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)|任务和组件都使用相同的 VSTA IDE，并且支持在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 中编写代码。|  
|预编译的脚本|从 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 开始，所有脚本都要进行预编译。 在早期版本中，您可以指定是否对脚本进行预编译。<br /><br /> 脚本被预编译为二进制代码会使执行更加快速，但代价是会增加包大小。|  
|调试|任务和组件都支持在设计环境中进行调试时设置断点和单步执行代码。 有关详细信息，请参阅[编码和调试脚本任务](../control-flow/script-task.md)和 [编码和调试脚本组件] (.../ extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md。|  
  
## <a name="differences-between-the-script-task-and-the-script-component"></a>脚本任务和脚本组件之间的不同之处  
 脚本任务和脚本组件有以下值得注意的不同之处。  
  
|功能|脚本任务|脚本组件|  
|-------------|-----------------|----------------------|  
|控制流/数据流|脚本任务在设计器的“控制流”选项卡中配置，在包的数据流外部运行。|脚本组件在设计器的“数据流”页中配置，表示数据流任务中的源、转换或目标。|  
|用途|脚本任务可完成几乎所有一般用途的任务。|必须指定是否要使用脚本组件创建源、转换或目标。|  
|执行|脚本任务在包工作流中的某个点运行自定义代码。 除非将其放在循环容器或事件处理程序中，否则它只运行一次。|脚本组件也运行一次，但是通常它为数据流中的每行数据运行一次主处理例程。|  
|编辑器|“脚本任务编辑器”有三个页面：“常规”、“脚本”和“表达式”。 仅`ReadOnlyVariables`和`ReadWriteVariables`，和**ScriptLanguage**属性直接影响你可以编写的代码。|“脚本转换编辑器”最多有四个页面：“输入列”、“输入和输出”、“脚本”和“连接管理器”。 在其中每个页面上配置的元数据和属性将决定自动生成以供您在编码中使用的基类的成员。|  
|与包交互|在为脚本任务编写的代码中，使用 `Dts` 属性访问包的其他功能。 `Dts` 属性是 `ScriptMain` 类的成员。|在脚本组件代码中，使用类型化的取值函数属性访问特定包功能，如变量和连接管理器。<br /><br /> `PreExecute` 方法仅可访问只读变量。 `PostExecute` 方法既可以访问只读变量，又可以访问读/写变量。<br /><br /> 有关这些方法的详细信息，请参阅 [编码和调试脚本组件] (.../ extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md。|  
|使用变量|脚本任务使用 `Dts` 对象的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 属性访问具备任务的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> 和 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> 属性的变量。 例如：<br /><br /> **[VB]**<br /><br /> `Dim myVar as String myVar = Dts.Variables(“MyStringVariable”).Value.ToString`<br /><br /> <br /><br /> **[C#]**<br /><br /> `string myVar; myVar = Dts.Variables["MyStringVariable"].Value.ToString();`|脚本组件使用自动生成的基类的类型化取值函数属性，这些属性基于组件的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> 属性创建。 例如：<br /><br /> **[VB]**<br /><br /> `Dim myVar as String myVar = Me.Variables.MyStringVariable`<br /><br /> <br /><br /> **[C#]**<br /><br /> `string myVar; myVar = this.Variables.MyStringVariable;`|  
|使用连接|脚本任务使用 `Dts` 对象的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 属性访问在包中定义的连接管理器。 例如：<br /><br /> **[VB]**<br /><br /> `Dim myFlatFileConnection As String myFlatFileConnection = _     DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _     String)`<br /><br /> <br /><br /> **[C#]**<br /><br /> `string myFlatFileConnection; myFlatFileConnection = (Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);`|脚本组件使用自动生成的基类的类型化取值函数属性，这些属性基于用户在编辑器的“连接管理器”页上输入的连接管理器列表创建。 例如：<br /><br /> **[VB]**<br /><br /> `Dim connMgr As IDTSConnectionManager100 connMgr = Me.Connections.MyADONETConnection`<br /><br /> <br /><br /> **[C#]**<br /><br /> `IDTSConnectionManager100 connMgr; connMgr = this.Connections.MyADONETConnection;`|  
|引发事件|脚本任务使用 `Dts` 对象的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> 属性引发事件。 例如：<br /><br /> **[VB]**<br /><br /> `Dts.Events.FireError(0, "Event Snippet", _     ex.Message & ControlChars.CrLf & ex.StackTrace, _     "", 0)`<br /><br /> <br /><br /> **[C#]**<br /><br /> `Dts.Events.FireError(0, "Event Snippet", ex.Message + "\r" + ex.StackTrace, "", 0);`|脚本组件使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 属性返回的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 接口的方法引发错误、警告和信息性消息。 例如：<br /><br /> **[VB]**<br /><br /> `Dim myMetadata as IDTSComponentMetaData100 myMetaData = Me.ComponentMetaData myMetaData.FireError(...)`|  
|日志记录|脚本任务使用<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>方法`Dts`启用日志提供程序的对象来记录到的信息。 例如：<br /><br /> **[VB]**<br /><br /> `Dim bt(0) As Byte Dts.Log("Test Log Event", _     0, _     bt)`<br /><br /> <br /><br /> **[C#]**<br /><br /> `byte[] bt = new byte[0]; Dts.Log("Test Log Event", 0, bt);`|脚本组件使用自动生成的基类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法将信息记录到已启用的日志提供程序。 例如：<br /><br /> **[VB]**<br /><br /> `Dim bt(0) As Byte`<br /><br /> `Me.Log("Test Log Event", _`<br /><br /> `0, _`<br /><br /> `bt)`<br /><br /> <br /><br /> **[C#]**<br /><br /> `byte[] bt = new byte[0]; this.Log("Test Log Event", 0, bt);`|  
|返回结果|脚本任务使用这两个<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A>属性和可选<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>属性`Dts`对象通知运行时在其结果。|脚本组件作为数据流任务的组成部分运行，不会使用这两个属性中的任何一个报告结果。|  
  
## <a name="see-also"></a>请参阅  
 [使用脚本任务扩展包](task/extending-the-package-with-the-script-task.md)   
 [使用脚本组件扩展数据流](data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
 [使用 SSIS 使用脚本 （策展答案） 中的 Web 服务](http://go.microsoft.com/fwlink/?LinkId=321996)  
  
  