---
title: 打印报表（报表生成器）| Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: b96936c9-c387-41a9-8c19-6eb325769ffd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ec88487e55015edcea264e3530ad13f732ca5fc9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "77082520"
---
# <a name="print-a-report-report-builder-and-ssrs"></a>打印报表（报表生成器和 SSRS）
  在将报表保存到报表服务器之后，可以通过浏览器、Reporting Services Web 门户或用于查看导出报表的任意应用程序查看和打印报表。 在保存报表之前，可以在预览报表时打印它。  
  
 打印报表时，可以指定所用纸张的大小。 纸张的大小决定了报表的页数以及适合每一页的报表数据。 纸张大小仅影响通过硬分页呈现器呈现的报表：PDF、Image 和 Print。 设置纸张大小不影响其他呈现器。 有关详细信息，请参阅[呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
 在 Reporting Services Web 门户中的“报表查看器”工具栏或报表设计器中的“预览”中，可以将报表导出到硬分页呈现器或单击“打印”按钮来打印报表的副本。 您可能需要设置纸张大小或其他页面设置属性。 使用 **“报表属性”** 对话框可以更改页面设置属性，包括纸张大小。  
  
 可以在以下两个不同位置指定打印页边距：在设计模式下和在运行模式下。  
  
-   **设计模式：** 如果设计模式下设置页边距，则保存报表时，这些设置会保存在报表定义中。  
  
-   **运行模式：** 如果在运行模式下设置页边距，则此信息不会保存在报表定义中。 下一次打印报表时，将从报表定义中获取设置，除非再次指定打印边距。  
  
    > [!NOTE]  
    >  在设计模式或运行模式下不会显示打印边距。 报表的设计图面区域和打印区域之间没有任何关系。 若要在运行模式下查看打印边距，请在功能区的 **“运行”** 选项卡上单击“打印布局”。  
  
 有关报表分页的详细信息，请参阅 [Reporting Services 中的分页（报表生成器和 SSRS）](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-print-a-report-in-report-builder"></a>在报表生成器中打印报表  
  
1.  打开报表。  
  
2.  在“主文件夹”选项卡上，单击 **“运行”** 。  
  
3.  （可选）单击“打印布局”以查看报表打印时的显示形式  。  
  
4.  （可选）单击“页面设置”以设置纸张、方向和边距  。  
  
    > [!NOTE]  
    >  以上各项的默认值均源自在“设计”视图中设置的报表属性。 此处您在 **“页面设置”** 对话框中所设置的值仅适用于此次会话。 当关闭此报表并将其重新打开时，它将再次恢复默认值。  
  
5.  单击 **“打印”** 。  
  
6.  在 **“打印”** 对话框中，选择打印机并指定其他打印选项。  
  
### <a name="to-print-a-report-from-a-web-browser-application"></a>从 Web 浏览器应用程序打印报表  
  
1.  在 Reporting Services Web 门户中，导航到要打印的报表。 打开该报表。  
  
3.  在报表顶部的工具栏上，单击 **“打印”** 。  
  
    > [!NOTE]  
    >  首次打印 HTML 报表时，报表服务器会提示您安装用于打印的 ActiveX 控件。 必须安装并配置该控件才能进行打印。  
  
4.  在 **“打印”** 对话框中，选择打印机，再单击 **“打印”** 。  
  
### <a name="to-print-a-report-from-other-applications"></a>从其他应用程序打印报表  
  
1.  在 Reporting Services Web 门户中，导航到要打印的报表。 打开该报表。  
  
2.  在报表顶部的工具栏上，选择呈现格式，再单击 **“导出”** 。 报表在与该呈现格式相对应的查看器应用程序中打开。  
  
     例如，如果选择 PDF，则报表在 Adobe Acrobat Reader 中打开。  
  
3.  在该程序的 **“文件”** 菜单上，单击 **“打印”** 。  
  
### <a name="to-change-paper-size"></a>更改纸张大小  
  
1.  右键单击表体外部区域，然后单击“报表属性”  。  
  
2.  在 **“页面设置”** 中，从 **“纸张大小”** 列表选择一个值。 每一选项都会填充 **“宽度”** 和 **“高度”** 属性。 您也可以通过在 **“宽度”** 和 **“高度”** 框中键入数值，来指定自定义大小。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  大小值的默认单位由用户的区域设置决定。 若要指定其他单位，请在提供的数字值后面键入一个物理单位指示符，例如 cm、mm、pt 或 pc。  
  
### <a name="to-set-page-margins-in-design-mode"></a>在设计模式下设置页边距  
  
-   右键单击设计图面周围的蓝色区域，单击“报表属性”，然后单击“页面设置”   页。  
  
### <a name="to-set-page-margins-in-run-mode"></a>在运行模式下设置页边距  
  
-   在 **“运行”** 选项卡上单击 **“页面设置”** 。  
  
## <a name="see-also"></a>另请参阅  
 [打印报表（报表生成器和 SSRS）](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [“报表属性”对话框，页面设置（报表生成器）](https://msdn.microsoft.com/library/eb3b5d01-7b82-4808-a58b-9e096742f8c6)   
 [报表设计视图（报表生成器）](../../reporting-services/report-builder/report-design-view-report-builder.md)  
  
  
