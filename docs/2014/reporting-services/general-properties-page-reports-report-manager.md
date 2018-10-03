---
title: 报表的常规属性页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 66c99d28-ab41-45f0-bf02-ed560293595d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e8606f2ee9afeb0e5e3ab0663290471b0d2d4463
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206157"
---
# <a name="general-properties-page-reports-report-manager"></a>报表的“常规”属性页（报表管理器）
  使用报表的“常规”属性页可以重命名、删除、移动或替换报表定义。 也可以使用此页创建链接报表。 页面顶部显示了有关创建或修改报表的用户以及发生更改的时间等详细信息。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-general-properties-page-for-a-report"></a>打开报表的“常规属性”页  
  
1.  打开报表管理器，找到您要查看或配置其属性的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”**。 这会打开该报表的“常规”属性页。  
  
## <a name="options"></a>选项  
 **名称**  
 指定报表的名称。 名称必须至少包含一个字母数字字符。 还可以包含空格和某些符号。 在指定名称时，不得使用字符 ; ? : \@ & = +，$ * \< >  
  
 " 和 /。  
  
 **Description**  
 键入报表的说明。 有权访问该报表的用户可以在“内容”页中查看此说明。  
  
 **在列表视图中隐藏**  
 选择此选项可对正在报表管理器中使用列表视图模式的用户隐藏报表。 列表视图模式是浏览报表服务器文件夹层次结构时的默认视图格式。 在列表视图中，项的名称和说明可跨越页面。 备用格式为详细信息视图。 详细信息视图省略了说明，但包含项的其他信息。 虽然可以在列表视图中隐藏项，但不能在详细信息视图中隐藏项。 如果希望限制访问项，必须创建角色分配。  
  
 **应用**  
 单击此选项可保存所做的更改。  
  
 **删除**  
 单击此选项可从报表服务器数据库中删除报表。 删除报表将删除所有关联的报表历史记录以及报表特定的计划和订阅。 如果链接报表与报表关联时，链接报表将失效。  
  
 **“移动”**  
 单击此选项可在报表服务器文件夹层次结构中重新定位报表。 单击此按钮将打开“移动项”页，可以在该页浏览文件夹以选择新的文件夹位置。 有关详细信息，请参阅[移动项页&#40;报表管理器&#41;](../../2014/reporting-services/move-items-page-report-manager.md)。  
  
 **创建链接的报表**  
 单击此选项可打开“新建链接报表”页。 有关此页和链接的报表的详细信息，请参阅[新链接报表页&#40;报表管理器&#41;](../../2014/reporting-services/new-linked-report-page-report-manager.md)。  
  
 **保存**  
 单击此选项可提取报表定义的只读副本。 根据计算机上所定义的文件关联，文件将在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 或其他应用程序中打开。 大多数情况下，报表将以 XML 文件形式打开。  
  
 您打开的副本与最初发布到报表服务器的原始报表定义相同。 在报表发布后对其设置的任何属性（例如参数和数据源属性）不会反映在您打开的文件中。  
  
 您可以修改报表定义并将其保存为共享文件夹中的新文件，再将报表定义作为新项上载到报表服务器。 在中打开时，报表定义所做的修改[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]（或另一个应用程序） 会不直接保存到报表服务器。 您必须通过上载文件将修改后的报表发布到报表服务器上。  
  
 **替换**  
 单击此选项可将当前报表中所使用的报表定义替换为文件系统上 .rdl 文件中的其他报表定义。 如果更新报表定义，则必须在更新完成后重置数据源设置。  
  
 **更改链接**  
 单击此选项可为链接报表选择其他报表定义。 当报表为链接报表时，将会显示此选项。 如果报表为链接报表，您可以设置此属性来替换报表定义。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器&#40;SSRS 本机模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
