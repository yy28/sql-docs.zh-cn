---
title: "通过在脚本任务和脚本组件中设置断点调试脚本 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 96815b337311c4ba8d16e10c25891c728e7a0c74
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a>通过在脚本任务和脚本组件中设置断点来调试脚本
  此过程描述如何在脚本任务和脚本组件所使用的脚本中设置断点。  
  
 在脚本中，设置了断点后**设置断点的\<对象名称 >**对话框中列出的断点，以及内置的断点。  
  
> [!IMPORTANT]  
>  在某些情况下，将忽略脚本任务和脚本组件中的断点。 有关详细信息，请参阅**Debugging the Script Task**主题中[编码和调试脚本任务](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)和**Debugging the Script Component**主题中[编码和调试脚本组件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="to-set-a-breakpoint-in-script"></a>在脚本中设置断点  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  双击包含要在其中设置断点的脚本的包。  
  
3.  若要打开脚本任务，请单击**控制流**选项卡上，然后双击脚本任务。  
  
4.  若要打开脚本组件，请单击**数据流**选项卡上，然后双击脚本组件。  
  
5.  单击**脚本**，然后单击**编辑脚本**。  
  
6.  在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)，找到你要在其设置断点，右键单击该行，指向的脚本行**断点**，然后单击**插入断点**。  
  
     断点图标随即出现在该行代码上。  
  
7.  在 **“文件”** 菜单中，单击 **“退出”**。  
  
8.  单击 **“确定”**。  
  
9. 若要保存包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
  

