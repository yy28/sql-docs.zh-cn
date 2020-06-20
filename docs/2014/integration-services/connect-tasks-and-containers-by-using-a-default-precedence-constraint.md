---
title: 使用默认优先约束来连接任务和容器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- precedence constraints [Integration Services], connecting tasks
- default precedence constraints
- containers [Integration Services], precedence constraints
ms.assetid: 8f31f15f-98ff-4c35-b41f-8b8cfd148d75
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b41330bcb2fe007b1f666382719f98d39ec67438
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921351"
---
# <a name="connect-tasks-and-containers-by-using-a-default-precedence-constraint"></a>使用默认优先约束来连接任务和容器
  优先约束连接两个可执行文件。 可执行文件可以是任何任务，也可以是 For 循环容器、Foreach 循环容器或序列容器。 此过程介绍如何设置优先约束的默认行为，以及如何用默认优先约束来连接可执行文件。  
  
## <a name="creating-default-precedence-constraints"></a>创建默认优先约束  
 首次使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器时，优先约束的默认值为 `Success`。 按照下列步骤将 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器配置为使用不同的优先约束默认值。  
  
#### <a name="to-set-the-default-value-for-precedence-constraints"></a>设置优先约束的默认值  
  
1.  打开 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
2.  在“工具”  菜单上，单击“选项” 。  
  
3.  在 **“选项”** 对话框中，展开 **“商业智能设计器”** ，再展开 **“Integration Services 设计器”**。  
  
4.  单击 **“控制流自动连接”** ，并选择 **“将新形状连接到默认选中的形状”**。  
  
5.  在下拉列表中，选择“对新形状使用‘失败’约束”或“对新形状使用‘完成’约束”。********  
  
6.  单击“确定”。  
  
#### <a name="to-create-a-default-precedence-constraint"></a>创建默认优先约束  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  在 **“控制流”** 选项卡的设计图面上，单击任务或容器，并将其连接线拖动到要将优先约束应用到其上的可执行文件。  
  
5.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [优先约束](control-flow/precedence-constraints.md)   
 [使用快捷菜单设置优先约束的值](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [设置优先约束的属性](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)   
 [在优先约束中使用表达式](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
