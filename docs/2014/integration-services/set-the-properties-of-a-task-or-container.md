---
title: 设置任务或容器的属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], properties
ms.assetid: 52d47ca4-fb8c-493d-8b2b-48bb269f859b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 278ce3d1a7f1fafeb3c378559e5ec88da62895c8
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421464"
---
# <a name="set-the-properties-of-a-task-or-container"></a>设置任务或容器的属性
  可以使用 **“属性”** 窗口设置任务和容器的大多数属性。 但任务集合的属性以及因过于复杂而无法使用 **“属性”** 窗口设置的属性不在此列。 例如，不能在 **“属性”** 窗口中配置 Foreach 循环容器使用的枚举器。 您必须使用任务或容器编辑器来设置这些复杂的属性。 大多数任务和容器编辑器都有多个节点，而每个节点都包含相关属性。 节点的名称指出了节点所包含属性的主题。  
  
 下面的过程介绍如何使用 **“属性”** 窗口或者任务或容器编辑器来设置相应任务或容器的属性。  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-the-properties-window"></a>使用“属性”窗口设置任务或容器的属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  在“控制流”选项卡的设计图面上，右键单击任务或容器，然后单击“属性”********。  
  
5.  在 **“属性”** 窗口中，更新属性值。  
  
    > [!NOTE]  
    >  大部分属性可以通过直接在文本框中键入值或者从列表中选择值的方式进行设置。 但是，某些属性比较复杂，并且具有自定义的属性编辑器。 若要设置属性，请在文本框中单击，然后单击生成按钮 (…) 打开自定义编辑器****。  
  
6.  也可以创建属性表达式来动态更新任务或容器的属性。 有关详细信息，请参阅 [添加或更改属性表达式](expressions/add-or-change-a-property-expression.md)。  
  
7.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-a-task-or-container-editor"></a>使用任务或容器编辑器设置任务或容器的属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  在“控制流”选项卡的设计图面上，右键单击任务或容器，然后单击“编辑”以打开相应的任务或容器编辑器********。  
  
     有关如何配置 For 循环容器的信息，请参阅[配置 For 循环容器](control-flow/for-loop-container.md)。  
  
     有关如何配置 Foreach 循环容器的信息，请参阅 [配置 Foreach 循环容器](control-flow/foreach-loop-container.md)。  
  
    > [!NOTE]  
    >  序列容器没有自定义编辑器。  
  
5.  如果任务或容器编辑器具有多个节点，单击包含要设置的属性的节点。  
  
6.  根据需要，也可以单击 **“表达式”** ，并在 **“表达式”** 页上创建属性表达式，以动态更新任务或容器的属性。 有关详细信息，请参阅 [添加或更改属性表达式](expressions/add-or-change-a-property-expression.md)。  
  
7.  更新属性值。  
  
8.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 任务](control-flow/integration-services-tasks.md)   
 [Integration Services 容器](control-flow/integration-services-containers.md)  
  
  
