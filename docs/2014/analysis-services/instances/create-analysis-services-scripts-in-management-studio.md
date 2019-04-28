---
title: 在 Management Studio 中创建 Analysis Services 脚本 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services objects, scripts
- objects [Analysis Services], scripts
- scripts [Analysis Services], objects
ms.assetid: 4f1b965c-9ca6-427b-8f4d-0ce1eea7c0fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d419a09c34998165f13fbc9e43c9b561602b69aa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730200"
---
# <a name="create-analysis-services-scripts-in-management-studio"></a>在 Management Studio 中创建 Analysis Services 脚本
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 包括您可以用来对 Analysis Services 对象和任务编写脚本的脚本生成功能、模板和编辑器。  
  
## <a name="script-analysis-services-tasks-in-management-studio"></a>在 Management Studio 中编写 Analysis Services 任务的脚本  
 通过单击面向任务的对话框中的某一个脚本选项，可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中编写任务脚本。 用来执行备份或还原数据库、处理对象或设计聚合之类的任务的所有对话框都在顶部包括一个脚本选项。 选择其中一个选项可以根据对话框中的信息和设置生成一个 XMLA 脚本。  
  
 默认情况下，在 XMLA 查询编辑器中生成并放置脚本，但是您也可以扩展脚本选项列表，将脚本保存到 Windows 剪贴板或某个文件中。  
  
#### <a name="to-script-an-analysis-services-task"></a>编写 Analysis Services 任务脚本  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例。  
  
2.  右键单击某个数据库，然后单击“备份”。 这将打开“备份数据库”对话框。 指定备份文件的名称，并选择要用于此备份的选项。  
  
3.  单击对话框顶部的 **“脚本”** 。 脚本功能是 Management Studio 中所有基于任务的对话框的一部分。 它具有以下选项：**脚本操作在新查询窗口**以打开查询编辑器窗口中，**操作脚本保存到文件**若要将 XMLA 脚本保存到一个文件，或**操作脚本保存到剪贴板**保存到 XMLA 脚本剪贴板。  
  
     请注意，Analysis Services 脚本不支持在 Management Studio 中列为脚本选项的 **“将操作脚本保存到作业”** 选项。  
  
4.  如果选择默认选项 **“将操作脚本保存到‘新建查询’窗口”**，生成的脚本将放置在 XMLA 查询窗口中。  
  
     您现在可以关闭“备份数据库”对话框，并编辑或直接运行 XMLA 脚本。  
  
## <a name="script-analysis-services-objects-in-management-studio"></a>在 Management Studio 中编写 Analysis Services 对象的脚本  
 可通过下列方法在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中编写对象脚本：右键单击 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象，然后选择“Create 到”、“Alter 到”或“Delete 到”。 这些选项中的每一个都可定向到窗口或文件，但是无论脚本定向到何处，它都会以 DDL 脚本或 XMLA 包装的形式出现。 此类脚本的一个突出优点就是可以在其指向的任何服务器中运行。 此外，脚本中的名称可以更改，并可针对大规模的构造、修改或删除对象进行迭代运行。  
  
 您可以编写脚本的对象包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的元素，具体包括数据源、数据源视图、多维数据集、维度、挖掘结构和角色。  
  
 前提条件是要对 XML for Analysis (XMLA) 有所了解。 幸运的是， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中具有自动创建 XMLA 脚本（用于创建多维数据集之类的对象）的功能。 该自动化功能可帮助在学习 XMLA 时少走弯路。 有关如何使用 XMLA 的详细信息，请参阅 [在 Analysis Services 中使用 XMLA 开发](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)。 有关如何使用 XMLA 的详细信息，请参阅 [在 Analysis Services 中使用 XMLA 开发](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)。  
  
> [!IMPORTANT]  
>  编写 Role 对象的脚本时，需要注意安全权限包含在这些权限保护的对象中，而非包含在与这些权限关联的安全角色中。  
  
#### <a name="to-script-analysis-services-objects"></a>编写 Analysis Services 对象脚本  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例。  
  
2.  找到要为其创建脚本（该脚本可以创建、更改或删除对象）的对象。  
  
3.  右键单击该对象，指向**作为多维数据集脚本**，依次指向**创建到**， **ALTER 到**，或**删除到**，然后单击其中一个以下选项：**新查询编辑器窗口**以打开查询编辑器窗口中，**文件**若要将 XMLA 脚本保存到一个文件，或**剪贴板**将 XMLA 脚本保存到剪贴板。  
  
    > [!NOTE]  
    >  通常，如果想要创建该文件的多个不同版本，请选择“文件”。  
  
## <a name="see-also"></a>请参阅  
 [在 Analysis Services 中编写管理任务脚本](../script-administrative-tasks-in-analysis-services.md)   
 [XMLA 查询编辑器（Analysis Services - 多维数据）](../xmla-query-editor-analysis-services-multidimensional-data.md)  
  
  
