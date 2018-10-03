---
title: 将报表导出为其他文件类型 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: b577568b-ecbd-44c3-be88-31dab6fc38a2
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0704648805ce9538e16ec504a8c3508b71f1c6ce
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48053737"
---
# <a name="export-a-report-as-another-file-type-report-builder-and-ssrs"></a>将报表导出为其他文件类型（报表生成器和 SSRS）
  在报表生成器或报表设计器中预览报表时，可以将报表呈现为其他文件格式，如 CSV、图像、PDF、[!INCLUDE[ofprword](../includes/ofprword-md.md)] 或 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]；也可以在查看报表服务器上的报表时呈现报表。 如果希望立即将报表另存为其他文件类型而不将报表发布到报表服务器，或者希望查看报表设计在以特定格式传递给报表读者时的显示效果，则以特定格式呈现报表将非常有用。 在设置订阅或通过电子邮件传递报表时，或者希望保存报表服务器上可用的报表时，呈现报表服务器上的报表将非常有用。 有关详细信息，请参阅[订阅和传递 (Reporting Services)](subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-export-a-report-as-another-file-type-in-report-builder"></a>在报表生成器中将报表导出为其他文件类型  
  
1.  预览报表。  
  
2.  在功能区上，单击 **“导出”**。  
  
3.  选择要使用的格式。  
  
     将打开 **“另存为”** 对话框。 默认情况下，文件名为所导出报表的名称。 也可更改该文件名。  
  
4.  导航到保存导出报表的位置并打开此报表。  
  
> [!NOTE]  
>  如果由于您没有与此文件类型关联的程序而导致程序无法以所选格式打开此报表，系统会提示您保存导出的报表或在线查找可打开此报表的程序。  
  
### <a name="to-export-a-report-as-another-file-type-in-report-manager"></a>在报表管理器中将报表导出为其他文件类型  
  
1.  从报表管理器的 **“主页”** 导航至要导出的报表。  
  
2.  单击该报表。  
  
     即会生成该报表。  
  
3.  在报表查看器工具栏上，单击 **“选择格式”** 下拉箭头。  
  
4.  选择要使用的格式。  
  
5.  单击 **“导出”**。  
  
     将出现一条消息，询问是要打开还是要保存该文件。  
  
6.  若要以选定的导出格式查看该报表，请单击 **“打开”**。  
  
     \- 或 -  
  
     若要立即以选定的导出格式保存该报表，请单击 **“保存”**。  
  
     将使用与所选格式关联的应用程序显示或保存该报表。 如果单击 **“保存”**，系统将提示您指定保存报表的位置。  
  
     **注意** 如果因没有与此文件类型关联的程序而导致程序无法以您所选的格式打开此报表，系统会提示您保存导出的报表或在线查找可打开此报表的程序。  
  
### <a name="to-export-a-report-as-another-file-type-in-a-sharepoint-library"></a>在 SharePoint 库中将报表导出为其他文件类型  
  
1.  预览报表。  
  
2.  在工具栏上，单击 **“操作”**，指向 **“导出”**，然后选择要使用的格式。  
  
     将打开 **“文件下载”** 对话框。  
  
3.  若要以选定的导出格式查看该报表，请单击 **“打开”**。  
  
     \- 或 -  
  
     若要立即以选定的导出格式保存该报表，请单击 **“保存”**。  
  
     将使用与所选格式关联的应用程序显示或保存该报表。 如果单击 **“保存”**，系统将提示您指定保存报表的位置。  
  
     还可以选择更改导出的报表的文件名。  
  
     **注意** 如果因没有与此文件类型关联的程序而导致程序无法以您所选的格式打开此报表，系统会提示您保存导出的报表或在线查找可打开此报表的程序。  
  
## <a name="see-also"></a>请参阅  
 [导出报表&#40;报表生成器和 SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)   
 [Reporting Services 中的分页（报表生成器和 SSRS）](report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [不同报表呈现扩展插件的交互功能&#40;报表生成器和 SSRS&#41;](report-builder/interactive-functionality-different-report-rendering-extensions.md)  
  
  
