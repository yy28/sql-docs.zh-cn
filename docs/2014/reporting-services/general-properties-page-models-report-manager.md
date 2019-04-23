---
title: 常规属性页中，模型 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.general.f1
ms.assetid: 7ad59850-8135-4c4d-95e9-6d705b6d77a8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2523909f2719fb8316acecf8ad0b56ddbe086a36
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59947543"
---
# <a name="general-properties-page-models-report-manager"></a>模型的“常规”属性页（报表管理器）
  使用报表模型的“常规”属性页可以重命名、删除、移动或替换模型定义 (.smdl) 文件。 页面顶部显示了有关创建或修改模型的用户以及发生更改的时间等详细信息。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-general-properties-page-for-a-model"></a>打开模型的“常规属性”页  
  
1.  打开报表管理器，找到您要查看或配置其属性的模型。  
  
2.  悬停在该模型之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”**。 这会打开该模型的“常规属性”页。  
  
## <a name="options"></a>选项  
 **名称**  
 指定模型的名称。 名称必须至少包含一个字母数字字符。 还可以包含空格和某些符号。 在指定名称时请不要使用以下字符：  
  
 ; ? : \@ & = + , $ / * \< > | " /  
  
 **说明**  
 键入模型的说明。 有权访问该模型的用户可以在“内容”页中查看此说明。  
  
 **在列表视图中隐藏**  
 在将文件夹设置为列表视图时，选中此复选框可以隐藏项。 列表视图是报表管理器支持的一种查看文件夹内容的模式。 可以在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中设置此选项，以定义在报表管理器中查看此项的方式。 有关视图模式在报表管理器的详细信息，请参阅[内容页&#40;报表管理器&#41;](../../2014/reporting-services/contents-page-report-manager.md)。  
  
 **Apply**  
 单击此选项可保存所做的更改。  
  
 **删除**  
 单击此选项可从报表服务器数据库中删除模型。 删除模型时，不会删除可提供连接信息的依赖共享数据源，也不会删除将该模型作为数据源的报表。 但是，在删除该模型后，使用该模型的报表将不再运行。  
  
 **“移动”**  
 单击此选项可在报表服务器文件夹层次结构中重新定位模型。 单击此按钮将打开“移动项”页，可以在该页浏览文件夹以选择新的文件夹位置。 有关详细信息，请参阅[移动项页&#40;报表管理器&#41;](../../2014/reporting-services/move-items-page-report-manager.md)。  
  
 **保存**  
 单击此选项可保存模型定义的只读副本。 根据计算机上所定义的文件关联，文件将在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 或其他应用程序中打开。 大多数情况下，模型将以 XML 文件形式打开。  
  
 您打开的副本与最初发布到报表服务器的原始模型定义相同。 在模型发布后对其设置的任何属性（如数据源属性）不会反映在您打开的文件中。  
  
 您可以修改模型定义并将其保存为共享文件夹中的新文件，再将模型定义作为新项上载到报表服务器。 当模型定义在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] （或其他应用程序）中处于打开状态时，对其进行的修改并不会直接保存到报表服务器上。 您必须上载文件以将修改后的模型发布到报表服务器上。  
  
 请注意，如果要在模型设计器中打开报表模型，则应当将该模型另存为 .smdl 文件，然后在模型设计器中将该 .smdl 文件添加到项目中。  
  
 **替换**  
 单击此选项可将模型定义替换为文件系统上 .smdl 文件中的其他模型定义。 如果更新模型定义，则必须在更新完成后重置共享数据源设置。  
  
 **重新生成模型**  
 单击此选项可重新生成替换当前版本的默认模型。 此选项会在生成模型之后出现。 所生成的模型将基于共享数据源。 在生成模型之前，不能对其进行自定义。 但是，在生成模型之后，可以单击 **“编辑”** 打开它的定义，将该定义保存到文件系统中，然后在模型设计器中将该定义添加到项目中。 在完善模型之后，可以将它作为新项上载到报表服务器，或者单击此页上的 **“更新”** 将所生成的模型替换为在模型设计器中修订的版本。  
  
## <a name="see-also"></a>请参阅  
 [将报表或模型绑定到共享数据源 (SSRS)](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Management Studio 中报表服务器的 F1 帮助](tools/report-server-in-management-studio-f1-help.md)  
  
  
