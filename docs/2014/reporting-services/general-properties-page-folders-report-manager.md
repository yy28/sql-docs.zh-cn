---
title: 常规属性页上，文件夹 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 31d99d9b-2303-4bae-9466-fb67b97cf11a
caps.latest.revision: 25
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9418474fed667dade02caaa7eb809ee8d2e16042
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083899"
---
# <a name="general-properties-page-folders-report-manager"></a>文件夹的“常规”属性页（报表管理器）
  使用文件夹的“常规”属性页可以查看和设置所创建文件夹的属性。 有关创建或修改文件夹的用户以及修改文件夹的时间的信息显示在“常规属性”页面顶部。  
  
 文件夹属性也包括安全性设置。 有关文件夹安全性的详细信息，请参阅[保护文件夹](security/secure-folders.md)。  
  
 不能在报表服务器命名空间中重命名或移动专用文件夹，例如主文件夹、我的报表和用户文件夹。 这些文件夹的“常规”属性页不可用。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-general-properties-page-for-a-folder"></a>打开文件夹的“常规属性”页  
  
1.  打开报表管理器，并打开您要查看或配置属性的文件夹。  
  
2.  在文件夹标志下，在工具栏中单击 **“文件夹设置”**。  
  
## <a name="options"></a>选项  
 **名称**  
 指定文件夹的名称。 名称必须至少包含一个字母数字字符。 还可以包含空格和某些符号。 在指定名称时，不得使用字符 ; ? : \@ & = +，$ * \< > |"或 / 指定名称时。  
  
 **Description**  
 键入对文件夹内容的说明。 有权访问该文件夹的用户可以在“内容”页中查看此说明。  
  
 **在列表视图中隐藏**  
 选择此选项可对正在报表管理器中使用列表视图模式的用户隐藏文件夹。 列表视图模式是浏览报表服务器文件夹层次结构时的默认视图格式。 在列表视图中，项的名称和说明可跨越页面。 备用格式为详细信息视图。 详细信息视图省略了说明，但包含项的其他信息。 虽然可以在列表视图中隐藏项，但不能在详细信息视图中隐藏项。 如果希望限制访问项，必须创建角色分配。  
  
 **应用**  
 单击此选项可保存所做的更改。  
  
 **删除**  
 单击此选项可删除文件夹及其内容。  
  
 **“移动”**  
 单击此选项可在报表服务器命名空间内重新定位报表或文件夹。 单击此按钮将打开“移动项”页，使用此页可以浏览文件夹以选择新的文件夹位置。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器&#40;SSRS 本机模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
