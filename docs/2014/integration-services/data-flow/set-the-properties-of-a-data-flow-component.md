---
title: 设置数据流组件的属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 61c56e88ef2124e2c8483ecaff778496840de2d0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37190827"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>设置数据流组件的属性
  若要设置数据流组件（包括源、目标和转换）的属性，请使用下列功能之一：  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的组件编辑器。 这些编辑器仅包含每个数据流组件的自定义属性。  
  
-   “属性”窗口列出每个元素的组件级自定义属性以及所有数据流元素通用的属性。  
  
-   通过 **“高级编辑器”** 对话框可以访问每个组件的自定义属性。 通过 **“高级编辑器”** 对话框，还可以访问所有数据流组件通用的属性，包括输入属性、输出属性、错误输出属性、列属性和外部列属性。  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-a-component-editor"></a>使用组件编辑器设置数据流组件的属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击“控制流”选项卡，然后双击数据流任务，此任务包含带有要查看和修改属性的组件的数据流。  
  
4.  双击数据流组件。  
  
5.  在组件编辑器中查看或修改属性值，然后关闭编辑器。  
  
6.  若要保存已更新的包，请在 **“文件”** 菜单中单击 **“保存选定项”**。  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-properties-window"></a>使用“属性”窗口设置数据流组件的属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击“控制流”选项卡，然后双击包含要查看和修改其属性的组件的数据流任务。  
  
4.  双击数据流组件，然后单击“属性”。  
  
5.  查看或修改属性值，然后关闭 **“属性”** 窗口。  
  
    > [!NOTE]  
    >  许多属性为只读，因此不能修改。  
  
6.  若要保存已更新的包，请在 **“文件”** 菜单中单击 **“保存选定项”**。  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-advanced-editor"></a>使用高级编辑器设置数据流组件的属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击“控制流”选项卡，然后双击包含要查看或修改的组件的数据流任务。  
  
4.  在数据流设计器中，右键单击数据流组件，然后单击“显示高级编辑器”。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，支持多个输入的数据流组件不能使用“高级编辑器”。  
  
5.  在 **“高级编辑器”** 对话框中，执行下列任意步骤：  
  
    -   若要查看和指定组件使用的连接，请单击 **“连接管理器”** 选项卡。  
  
        > [!NOTE]  
        >  “连接管理器”选项卡仅对使用连接管理器连接到数据源（如文件和数据库）的数据流组件可用  
  
    -   若要查看和修改组件级属性，请单击“组件属性”选项卡。  
  
    -   若要查看和修改外部列和可用输出之间的映射，请单击 **“列映射”** 选项卡。  
  
        > [!NOTE]  
        >  “列映射”选项卡仅在查看或编辑源或者目标时可用。  
  
    -   若要查看可用输入列的列表并更新输出列的名称，请单击 **“输入列”** 选项卡。  
  
        > [!NOTE]  
        >  输入列选项卡只在对转换或目标进行操作时可用。 有关详细信息，请参阅 [Integration Services Transformations](transformations/integration-services-transformations.md)。  
  
    -   若要查看和修改输入、输出和错误输出的属性以及它们包含的列的属性，请单击 **“输入属性和输出属性”** 选项卡。  
  
        > [!NOTE]  
        >  源没有输入。 除了一个可选错误输出之外，目标没有输出。  
  
6.  查看或修改属性值。  
  
7.  单击“确定” 。  
  
8.  若要保存已更新的包，请在 **“文件”** 菜单中单击 **“保存选定项”**。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 转换](transformations/integration-services-transformations.md)  
  
  
