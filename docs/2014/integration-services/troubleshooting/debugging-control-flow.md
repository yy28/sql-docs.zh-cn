---
title: 调试控制流 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- progress reporting [Integration Services]
- breakpoints [Integration Services]
- debugging [Integration Services], control flow
- control flow [Integration Services], debugging
- color-coded progress reporting [Integration Services]
- Set Breakpoints dialog box
ms.assetid: 54a458cc-9f4f-4b48-8cf2-db2e0fa7756c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 142a22e07a9abf5a87e63268910de35ff95b79ee
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216277"
---
# <a name="debugging-control-flow"></a>调试控制流
  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 并[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]包括功能和工具，可用来进行故障排除中的控制流[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]包。  
  
-   [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 支持容器和任务上的断点。  
  
-   [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器在运行时提供进度报告。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 提供了调试窗口。  
  
## <a name="breakpoints"></a>断点  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器提供了**设置断点**对话框，在其中你可以通过启用中断条件设置断点并挂起指定的包的执行之前可以发生断点的次数。 断点可在包级或单个组件级启用。 如果在任务或容器级上启用中断条件，则在 **“控制流”** 选项卡的设计图面上，相应的任务或容器旁边会显示断点图标。如果在包一级启用中断条件，则在 **“控制流”** 选项卡的标签上显示断点图标。  
  
 在命中断点时，断点图标将会发生改变以帮助识别断点源。 包运行时，可以添加、删除和更改断点。  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 提供了十个可以在所有任务和容器上启用的中断条件。 在 **“设置断点”** 对话框中，可根据下列条件启用断点：  
  
|中断条件|Description|  
|---------------------|-----------------|  
|当任务或容器收到`OnPreExecute`事件。|任务将要执行时调用。 此事件由任务或容器在其运行前一刻引发。|  
|当任务或容器收到`OnPostExecute`事件。|任务的执行逻辑完成后立即调用。 此事件由任务或容器在其运行后引发。|  
|当任务或容器收到`OnError`事件。|出现错误时由任务或容器调用。|  
|当任务或容器收到`OnWarning`事件。|当任务处于不能证明出错但有必要发出警告的状态时调用。|  
|当任务或容器收到`OnInformation`事件。|需要任务提供信息时调用。|  
|当任务或容器收到`OnTaskFailed`事件。|任务宿主失败时由其调用。|  
|当任务或容器收到`OnProgress`事件。|要更新任务执行的进度时调用。|  
|当任务或容器收到`OnQueryCancel`事件。|在可以取消执行的任务处理中，随时可以调用。|  
|当任务或容器收到`OnVariableValueChanged`事件。|变量值更改时，由 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 运行时调用。 变量的 RaiseChangeEvent 必须设置为`true`才能引发此事件。<br /><br /> **\*\* 警告 \*\*** 必须在 **容器** 作用域定义与此断点关联的变量。 如果在包作用域定义变量，则不会命中断点。|  
|当任务或容器收到`OnCustomEvent`事件。|由任务调用，用于引发自定义的任务定义事件。|  
  
 除了对所有任务和容器可用的中断条件外，有些任务和容器还包含用来设置断点的特殊中断条件。 例如，可以在 For 循环容器上启用中断条件，设置一个在循环的每个迭代开始时挂起执行的断点。  
  
 若要增加断点的灵活性和能力，可通过指定下列选项来修改断点的行为：  
  
-   命中计数，即执行挂起之前中断条件出现的最大次数。  
  
-   命中计数类型，或指定中断条件何时触发断点的规则。  
  
 命中计数类型（除“始终”类型以外）由命中计数进行进一步限定。 例如，如果类型是“命中计数等于”并且命中计数是 5，则在中断条件第六次出现时挂起执行。  
  
 下表介绍命中计数类型。  
  
|命中计数类型|Description|  
|--------------------|-----------------|  
|始终|断点命中时始终挂起执行。|  
|命中计数等于|断点发生的次数等于命中计数时挂起执行。|  
|命中计数大于或等于|断点发生的次数等于或大于命中计数时挂起执行。|  
|命中计数倍增基数|断点发生的次数为命中计数的倍数时挂起执行。 例如，如果将此选项设置为 5，则每命中五次就挂起执行。|  
  
#### <a name="to-set-breakpoints"></a>设置断点  
  
-   [通过在任务或容器上设置断点调试包](../debug-a-package-by-setting-breakpoints-on-a-task-or-a-container.md)  
  
## <a name="progress-reporting"></a>进度报告  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器包含两种类型进度报告：“控制流”选项卡设计图面上的颜色编码和“进度”选项卡上的进度消息。  
  
 运行包时， [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器使用可指示执行状态的颜色显示每个任务或容器，以此来描绘执行进度。 可根据颜色判断元素是否正在等待运行、是否当前正在运行、是否已成功完成或者已经以失败结束。 停止包执行后，颜色编码将消失。  
  
 下表介绍用于描绘执行状态的各种颜色。  
  
|Color|执行状态|  
|-----------|----------------------|  
|灰色|等待运行|  
|Yellow|正在运行|  
|绿色|成功运行|  
|已突出显示|运行，但有错误|  
  
 **“进度”** 选项卡上按执行顺序列出了任务和容器，并包含了开始时间和结束时间、警告以及错误信息。 停止包执行后，在 **“执行结果”** 选项卡上的进度信息仍然可用。  
  
> [!NOTE]  
>  若要允许或禁止在 **“进度”** 选项卡上显示消息，请在 **SSIS** 菜单上切换 **“调试进度报告”** 选项。  
  
 下面的关系图显示 **“进度”** 选项卡。  
  
 ![SSIS 设计器的“进度”选项卡](../media/mw-dtsflow04.gif "SSIS 设计器的“进度”选项卡")  
  
## <a name="debug-windows"></a>调试窗口  
 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 包含多个窗口，可以用来处理断点，以及用来调试包含断点的包。 若要了解每个窗口的更多信息，请打开该窗口，然后按 F1 显示该窗口的帮助。  
  
 若要在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中打开这些窗口，请单击 **“调试”** 菜单，指向 **“窗口”**，然后单击 **“断点”**、 **“输出”** 或 **“即时”**。  
  
 下表介绍这些窗口。  
  
|窗口|Description|  
|------------|-----------------|  
|断点|列出包中的断点并提供启用和删除断点的选项。|  
|“输出”|显示 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中各功能的状态消息。|  
|“即时”|用于调试和评估表达式，并打印变量值。|  
  
## <a name="see-also"></a>请参阅  
 [包开发的疑难解答工具](troubleshooting-tools-for-package-development.md)  
  
  
