---
title: 常规属性页上，资源 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 23eed41b-283a-49df-a3aa-062dde8d6354
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a6b4b76edb7eb7761511e39ba97b811dcf3d5e99
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63260673"
---
# <a name="general-properties-page-resources-report-manager"></a>资源的“常规”属性页（报表管理器）
  使用资源的“常规”属性页可以重命名、删除、移动或替换资源。 页面顶部显示有关添加资源或修改属性的用户的信息。  
  
 若要打开此页，请选择某个资源，再单击页面顶部的 **“属性”** 选项卡。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-general-properties-page-for-a-resource"></a>打开资源的“常规属性”页  
  
1.  打开报表管理器，找到您要查看或配置其属性的资源。  
  
2.  悬停在该资源之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”**。 这会打开该资源的“常规属性”页。  
  
## <a name="options"></a>选项  
 **名称**  
 指定资源的名称。 名称必须至少包含一个字母数字字符。 还可以包含空格和某些符号。 在指定名称时，不得使用字符 ; ? : \@ & = +，$ / * \< > |"或 / 指定名称时。  
  
 **说明**  
 键入资源的说明。 有权访问该资源的用户可以在“内容”页中看到此说明。  
  
 **在列表视图中隐藏**  
 选择此选项可对正在报表管理器中使用列表视图模式的用户隐藏资源。 列表视图模式是浏览报表服务器文件夹层次结构时的默认视图格式。 在列表视图中，项的名称和说明可跨越页面。 备用格式为详细信息视图。 详细信息视图省略了说明，但包含项的其他信息。 虽然可以在列表视图中隐藏项，但不能在详细信息视图中隐藏项。 如果希望限制访问项，必须创建角色分配。  
  
 **类型**  
 指定资源的 MIME 类型。 该属性为只读。  
  
 **Apply**  
 单击此选项可保存所做的更改。  
  
 **删除**  
 单击此选项可从报表服务器数据库中删除资源。  
  
 **“移动”**  
 单击此选项可在报表服务器文件夹层次结构中重新定位资源。 单击此按钮将打开“移动项”页，可以在该页浏览文件夹以选择新的文件夹位置。  
  
 **替换**  
 单击此选项可打开“导入资源”页，在该页上可以从文件共享中选择资源文件。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [查看资源的页&#40;报表管理器&#41;](../../2014/reporting-services/view-page-resources-report-manager.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [项的“安全性”属性页（报表管理器）](../../2014/reporting-services/security-properties-page-items-report-manager.md)  
  
  
