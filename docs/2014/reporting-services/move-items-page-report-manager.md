---
title: "\"移动项\" 页（报表管理器） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: fc83b8d2-bc79-4b56-8970-34a1cbbcc176
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f64a9e9efe180c2db776c38553403e5f7cdfac9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108216"
---
# <a name="move-items-page-report-manager"></a>“移动项”页（报表管理器）
  使用“移动项”页可以将报表、文件夹或其他项移至报表服务器上的新位置。 您可以键入新位置的路径，也可以使用树视图找到报表服务器命名空间中的新位置。 只能移动您有权移动并且存储在当前报表服务器中的项。  
  
 移动其他项所引用的项（例如，由许多报表引用的共享数据源或模型）时，该项的路径信息将自动更新。 移动共享数据源不会中断与使用它的报表和模型的数据源连接。 如果将共享数据源或模型移至用户无权访问的文件夹，则用户仍能够运行任何引用该数据源或模型的报表，但是用户在文件层次结构中看不到该项。  
  
 对于 **“位置”**，请指定文件夹的完整路径（以根文件夹名称开头）。 您可以键入路径名或使用树视图定位至所需的文件夹。  
  
> [!NOTE]  
>  并非所有的项都可以移动。 您不能移动保留文件夹，例如主文件夹、我的报表或用户文件夹。 也不能将报表历史记录或快照移至其他位置。 历史记录和快照应始终与它们所基于的报表位于相同的位置中，并且可以通过该报表进行访问。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-details-view"></a>从“详细信息视图”中的“内容”页打开“移动项”页  
  
1.  打开报表管理器，导航到包含要移动的项的文件夹。 您还可以移动报表管理器主页中的项。  
  
2.  在工具栏中，单击 **“详细信息视图”**。  
  
    > [!NOTE]  
    >  如果您只看到 **“平铺视图”**，则您已在 **“详细信息视图”** 中。  
  
3.  选择项旁边的框，然后单击工具栏中的 **“移动”** 。 如果您要将多个项移到同一个新位置，则可以选择多个框。  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-tiles-view"></a>从“平铺视图”中的“内容”页打开“移动项”页  
  
1.  打开报表管理器，导航到包含要移动的项的文件夹。 您还可以移动报表管理器主页中的项。  
  
2.  在工具栏中，单击 **“平铺视图”**。  
  
    > [!NOTE]  
    >  如果您只看到 **“详细信息视图”**，则您已在 **“平铺视图”** 中。  
  
3.  悬停在该项之上，然后单击下拉箭头。  
  
4.  在下拉菜单中，单击 **“移动”**。  
  
###### <a name="to-open-the-move-items-page-from-the-general-properties-page-of-an-item"></a>从项的“常规属性”页打开“移动项”页  
  
1.  打开报表管理器，导航到包含要移动的项的文件夹。 您还可以移动报表管理器主页中的项。  
  
2.  悬停在该项之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”** 。 这会打开项的“常规属性”页。  
  
4.  在项工具栏中，单击 **“移动”**。  
  
## <a name="see-also"></a>另请参阅  
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 ["常规属性" 页，文件夹 &#40;报表管理器&#41;](../../2014/reporting-services/general-properties-page-folders-report-manager.md)   
 [报表 &#40;报表管理器的 "常规属性" 页&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 ["常规属性" 页，报表管理器的资源 &#40;&#41;](../../2014/reporting-services/general-properties-page-resources-report-manager.md)   
 ["常规属性" 页，"共享数据源" &#40;报表管理器&#41;](../../2014/reporting-services/general-properties-page-shared-data-sources-report-manager.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
