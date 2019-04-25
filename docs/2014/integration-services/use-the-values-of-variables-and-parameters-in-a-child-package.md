---
title: 在子包中使用变量和参数的值 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- configurations [Integration Services]
- packages [Integration Services], configurations
- variables [Integration Services], adding
ms.assetid: 9b939edb-4e17-48e5-8428-855beb10049c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c1e942df4681595be19f31aa6a9d7c6fd3a6dd12
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766100"
---
# <a name="use-the-values-of-variables-and-parameters-in-a-child-package"></a>在子包中使用变量和参数的值
  此过程介绍如何创建使用父变量配置类型的包配置。 通过此配置类型，从父包运行的子包可以访问父包中的变量。  
  
> [!NOTE]  
>  您还可以通过配置执行包任务将值传递给子包，以将父包变量或参数（或项目参数）映射到子包参数。 有关详细信息，请参阅 [Execute Package Task](control-flow/execute-package-task.md)。  
  
 在子包中创建包配置之前，不必在父包中创建变量。 可以随时在父包中添加变量，但必须在包配置中使用准确的父变量名称。 但是，在配置可以更新的子包中必须有现成的变量，然后才能创建父变量配置。 有关添加和配置变量的详细信息，请参阅 [添加、删除、更改包中用户定义变量的作用域](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)。  
  
 父包中用于父变量配置的变量的作用域可以设置为“执行包”任务、包含任务的容器或包。 如果在包中定义了多个同名的变量，则使用在作用域中最接近“执行包”任务的变量。 最接近“执行包”任务的作用域是该任务本身。  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>向父包中添加变量  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含目标包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目，所谓目标包是指您想将要传递给子包的变量添加到其中的包。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，若要定义变量的作用域，请执行下列操作之一：  
  
    -   若要设置包的范围，请单击 **“控制流”** 选项卡设计图面上的任何位置。  
  
    -   若要将作用域设置为“执行包”任务的父容器，请单击该容器。  
  
    -   若要将作用域设置为“执行包”任务，请单击该任务。  
  
4.  添加并配置变量。  
  
    > [!NOTE]  
    >  选择与变量将要存储的数据兼容的数据类型。  
  
5.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
### <a name="to-add-a-variable-to-a-child-package"></a>向子包中添加变量  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，有一个 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目应当包含您要向其中添加父变量配置的包，请将该项目打开。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，若要设置包的作用域，请在 **“控制流”** 选项卡的设计图面上单击任何位置。  
  
4.  添加并配置变量。  
  
    > [!NOTE]  
    >  选择与变量将要存储的数据兼容的数据类型。  
  
5.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
### <a name="to-add-a-parent-package-configuration-to-a-child-package"></a>向子包添加父包配置  
  
1.  如果尚未打开它，请在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中打开子包。  
  
2.  在 **“控制流”** 选项卡的设计图面上单击任何位置。  
  
3.  在 **SSIS** 菜单上，单击 **“包配置”**。  
  
4.  在 **“包配置组织程序”** 对话框中，选择 **“启用包配置”**，再单击 **“添加”**。  
  
5.  在包配置向导的欢迎页中，单击 **“下一步”**。  
  
6.  在“选择配置类型”页上的 **“配置类型”** 列表中，选择 **“父包变量”** ，并执行下列操作之一：  
  
    -   选择 **“直接指定配置设置”**，然后在 **“父变量”** 框中提供要在配置中使用的父包中的变量的名称。  
  
        > [!IMPORTANT]  
        >  变量名称区分大小写。  
  
    -   选择“配置位置存储在一个环境变量中”，然后在“环境变量列表”中选择包含变量名称的环境变量。  
  
7.  单击“下一步” 。  
  
8.  在“选择目标属性”页上，展开 **“变量”** 节点，并展开要配置的变量的 **“属性”** 节点，然后单击要由配置设置的属性。  
  
9. 单击“下一步” 。  
  
10. （可选）在“完成向导”页上，修改配置的默认名称，并检查配置信息。  
  
11. 单击 **“完成”** 以完成向导并返回 **“包配置组织程序”** 对话框。  
  
12. 在 **“包配置组织程序”** 对话框中， **“配置”** 框将列出新配置。  
  
13. 单击 **“关闭”**。  
  
## <a name="see-also"></a>请参阅  
 [“包配置”](../../2014/integration-services/package-configurations.md)   
 [创建包配置](../../2014/integration-services/create-package-configurations.md)   
 [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)   
 [在包中使用变量](../../2014/integration-services/use-variables-in-packages.md)  
  
  
