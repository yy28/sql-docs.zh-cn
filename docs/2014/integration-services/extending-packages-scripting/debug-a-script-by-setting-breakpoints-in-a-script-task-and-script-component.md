---
title: 通过在脚本任务和脚本组件中设置断点来调试脚本 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6d3104a749db2099434bb5e3c2c0d8cde374f620
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52789409"
---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a>通过在脚本任务和脚本组件中设置断点来调试脚本
  此过程描述如何在脚本任务和脚本组件所使用的脚本中设置断点。  
  
 在脚本中设置断点后，“设置断点 - \<对象名称>”对话框会列出这些断点以及内置断点。  
  
> [!IMPORTANT]  
>  在某些情况下，将忽略脚本任务和脚本组件中的断点。 有关详细信息，请参阅**调试脚本任务**主题中[编码和调试脚本任务](../control-flow/script-task.md)并**调试脚本组件**[代码编写中的部分和调试脚本组件] (../ extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md。  
  
### <a name="to-set-a-breakpoint-in-script"></a>在脚本中设置断点  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  双击包含要在其中设置断点的脚本的包。  
  
3.  若要打开脚本任务，请单击“控制流”选项卡，然后双击该脚本任务。  
  
4.  若要打开脚本组件，请单击“数据流”选项卡，然后双击该脚本组件。  
  
5.  单击“脚本”，然后单击“编辑脚本”。  
  
6.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 中，找到要设置断点的脚本行，右键单击该行，指向“断点”，再单击“插入断点”。  
  
     断点图标随即出现在该行代码上。  
  
7.  在 **“文件”** 菜单中，单击 **“退出”**。  
  
8.  单击“确定” 。  
  
9. 若要保存包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
  
