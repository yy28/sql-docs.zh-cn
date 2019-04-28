---
title: 添加、 删除、 更改包中用户定义变量的作用域 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], adding
ms.assetid: cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 09f0b1ece44841cb608469cf2087041d20a9bf39
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62837265"
---
# <a name="add-delete-change-scope-of-user-defined-variable-in-a-package"></a>添加、删除、更改包中用户定义变量的作用域
  这些过程介绍如何使用“变量”窗口来添加、删除和更改包中用户定义变量的作用域。  
  
 有关变量作用域的详细信息，请参阅 [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)区域之下。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 还提供了可在运行时提供系统信息的系统变量，这些系统变量可在包和事件处理程序等容器中使用。 您无法删除系统变量。  
  
### <a name="to-add-a-variable"></a>添加变量  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要使用的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，若要定义变量的作用域，请执行下列操作之一：  
  
    -   若要设置包的范围，请单击 **“控制流”** 选项卡设计图面上的任何位置。  
  
    -   若要设置事件处理程序的作用域，请在 **“事件处理程序”** 选项卡的设计图面上，选择一个可执行文件和一个事件处理程序。  
  
    -   若要设置任务或容器的范围，请在 **“控制流”** 选项卡或 **“事件处理程序”** 选项卡的设计图面上，单击一个任务或容器。  
  
4.  在 **SSIS** 菜单上单击 **“变量”**。 您可以通过将 View.Variables 命令映射到在 **“选项”** 对话框的 **“键盘”** 页上选择的组合键来显示 **“变量”** 窗口。  
  
5.  在 **“变量”** 窗口中，单击 **“添加变量”** 图标。 新的变量将添加到该列表中。  
  
6.  也可以单击 **“网格选项”** 图标，选择要在 **“变量网格选项”** 对话框中显示的其他列，然后单击 **“确定”**。  
  
7.  或者，设置变量属性。 有关详细信息，请参阅 [设置用户定义变量的属性](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)。  
  
8.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
### <a name="to-delete-a-variable"></a>删除变量  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，右键单击该包将其打开。  
  
3.  在 **SSIS** 菜单上单击 **“变量”**。 您可以通过将 View.Variables 命令映射到在 **“选项”** 对话框的 **“键盘”** 页上选择的组合键来显示 **“变量”** 窗口。  
  
4.  选择要删除的变量，然后单击 **“删除变量”**。  
  
     如果在“变量”窗口中没有看到该变量，请单击“网格选项”，然后选择“显示所有作用域的变量”。  
  
5.  如果 **“确认删除变量”** 对话框打开，请单击 **“是”** 确认删除。  
  
6.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
### <a name="to-change-the-scope-of-a-variable"></a>更改变量的作用域  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，右键单击该包将其打开。  
  
3.  在 **SSIS** 菜单上单击 **“变量”**。 您可以通过将 View.Variables 命令映射到在 **“选项”** 对话框的 **“键盘”** 页上选择的组合键来显示 **“变量”** 窗口。  
  
4.  选择该变量，然后单击 **“移动变量”**。  
  
     如果在“变量”窗口中没有看到该变量，请单击“网格选项”，然后选择“显示所有作用域的变量”。  
  
5.  在 **“选择新作用域”** 对话框中，选择包或包中的容器、任务或事件处理程序，以更改变量作用域。  
  
6.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)   
 [在包中使用变量](../../2014/integration-services/use-variables-in-packages.md)   
 [设置用户定义变量的属性](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)   
 [在子包中使用变量和参数的值](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
  
