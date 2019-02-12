---
title: 常规属性页上，报表部件 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 93ddce72-31f1-42f7-abd5-8191acbb00c5
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a3872636fdfda37165bdf6cb83aa13aa51b230b2
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040478"
---
# <a name="general-properties-page-report-parts-report-manager"></a>报表部件的“常规”属性页（报表管理器）
  使用该属性页可以查看和管理报表部件的常规属性。  
  
 从报表管理器不能查看或更改报表部件的外观和功能。 若要更改设计，必须使用创作工具打开和修改设计，然后将其重新发布到服务器。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-properties-page-for-a-report-part"></a>打开报表部件的属性页  
  
1.  打开报表管理器，找到您要配置属性的报表部件。  
  
2.  悬停在该报表部件之上，然后单击下拉箭头。  
  
3.  在下拉列表中，单击 **“管理”**。 此时，将打开“常规”属性页。  
  
## <a name="options"></a>选项  
 **修改的日期**  
 上次在服务器上修改报表部件属性的日期和时间或上次将报表部件的新版本发布到服务器的日期和时间。 只读。  
  
 **修改者**  
 上次修改报表部件的用户名。 只读。  
  
 **创建日期**  
 最初将报表部件发布到服务器的日期和时间。 只读。  
  
 **创建的**  
 最初创建报表部件的用户名。 只读。  
  
 **大小**  
 报表部件的文件大小。 只读。  
  
 **名称**  
 键入一个名称来标识报表部件。  
  
 **说明**  
 提供有关报表部件的信息。 该说明显示在报表管理器的“内容”页中。 用户从报表创作工具中搜索报表部件时，可以搜索该说明文本。  
  
 **在列表视图中隐藏**  
 选择此选项可对正在报表管理器中使用列表视图模式的用户隐藏报表部件。 列表视图模式是浏览报表服务器文件夹层次结构时的默认视图格式。 虽然可以在列表视图中隐藏项，但不能在详细信息视图中隐藏项。 如果希望限制访问项，必须创建角色分配。  
  
 **类型**  
 报表部件的类型。 只读。  
  
 **应用**  
 保存更改。  
  
 **删除**  
 从报表服务器数据库中删除报表部件。 从服务器删除报表部件时，将不阻止已具有该报表部件的现有报表的呈现。  
  
 **“移动”**  
 单击以打开“移动项”页，在报表服务器文件夹层次结构中移动报表部件。 有关详细信息，请参阅[移动项页&#40;报表管理器&#41;](../../2014/reporting-services/move-items-page-report-manager.md)。  
  
 **下载**  
 提取要以 .rsc 文件形式保存的报表部件定义的副本。 .rsc 文件可以上载到报表服务器文件夹，或用于替换报表服务器文件夹中现有的报表部件。  
  
 **替换**  
 用 .rsc 文件中的另一个定义替换该报表部件定义。  
  
## <a name="see-also"></a>请参阅  
 [管理报表部件](report-design/managing-report-parts.md)   
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [“内容”页（报表管理器）](../../2014/reporting-services/contents-page-report-manager.md)   
 [报表部件（报表生成器和 SSRS）](report-parts-report-builder-and-ssrs.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [报表生成器中的报表部件和数据集](report-data/report-parts-and-datasets-in-report-builder.md)  
  
  
