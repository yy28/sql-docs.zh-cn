---
title: 向 URL 添加超链接（报表生成器和 SSRS）| Microsoft Docs
ms.date: 09/07/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 30514478f54d71d88245ace385600cb2931101eb
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/16/2018
ms.locfileid: "51814140"
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>向 URL 添加超链接（报表生成器和 SSRS）
了解如何在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  分页报表向文本框、图像、图表和仪表添加超链接操作。 链接可以转到其他报表、报表中的书签或是静态或动态 URL。 

 可以向具有“操作”属性的任何项添加超链接操作，例如图表中的文本框、图像或计算序列。 用户单击该报表项时，将执行您所定义的操作。  
  
*   可以 **添加将使用指定的 URL 打开浏览器的超链接** 。 该超链接既可以是静态 URL，也可以是计算结果为 URL 的表达式。 如果数据库中的某个字段包含 URL，则表达式可以包含该字段，从而为报表提供超链接的动态列表。 请确保报表读取器有权访问你提供的 URL。  
   
*  如果你和你的用户有权使用对报表服务器的 URL 请求来查看某一报表服务器上的报表，则你还可以 **指定用于对这些报表创建钻取的 URL** 。 例如，可以指定一个报表，并在用户首次查看该报表时隐藏文档结构图。 有关详细信息，请参阅 [URL 访问 (SSRS)](../../reporting-services/url-access-ssrs.md) 和[指定外部项的路径（报表生成器和 SSRS）](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)。
 
 *  并且你可以在相同报表中 **向特定位置添加书签** 。 
  
尝试使用[教程：设置文本格式（报表生成器）](../../reporting-services/tutorial-format-text-report-builder.md)中的示例数据添加超链接。  
  
> [!NOTE]  
>  绑定到数据集字段的链接容易被篡改。 有关详细信息，请参阅 [保护报表和资源](../../reporting-services/security/secure-reports-and-resources.md)。  
  
## <a name="to-add-a-hyperlink-and"></a>添加超链接和...   
  
1.  在报表设计视图中，右键单击要添加链接的文本框、图像或图表，然后单击 **“属性”**。  
  
2.  在“属性”对话框中，单击“操作”选项卡。阅读有关选项的信息。  

## <a name="-add-drillthrough-to-another-report"></a>...向其他报表添加钻取

1. 在“操作”选项卡上，选择“转到报表”。 

2. 指定要使用的目标报表和参数。 参数名称必须与为目标报表定义的参数相匹配。 

3. 使用“添加”和“删除”按钮可添加和删除参数，使用向上键和向下键可对参数列表进行排序。

4.  键入或选择要传递给钻取报表中的命名参数的“值”。 单击“表达式”(fx) 按钮可编辑表达式。

5. 选择“省略”可阻止参数运行。 默认情况下，此复选框已清除，处于不活动状态。 若要选中该复选框，请单击“表达式”(fx) 按钮，然后输入 True 或创建表达式。 当单击“表达式”对话框中的“确定”时，即会选中此复选框。
  
   有关详细信息，请参阅 [在报表中添加钻取操作](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) 。 
   
6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
   
## <a name="-add-a-bookmark"></a>...添加书签

可以将书签链接到当前报表中的某个位置。 若要链接到书签，首先必须设置报表项的“书签”属性。 若要设置“书签”属性，请选择一个报表项并在“属性”窗格中键入书签 ID 的值或表达式；例如，SalesChart 或 5TopSales。

1. 在“操作”选项卡上，选择“转到书签”。 

2. 输入或选择要跳至的报表的书签 ID。 单击表达式 (fx) 按钮可更改表达式。 

   书签 ID 可以是静态 ID，也可以是计算结果为书签 ID 的表达式。 表达式中可以包括含有书签 ID 的字段。
   
   有关详细信息，请参阅 [向报表添加书签](../../reporting-services/report-design/add-a-bookmark-to-a-report-report-builder-and-ssrs.md) 。
   
3. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="-add-a-hyperlink"></a>...添加超链接 
  
1. 在“操作”选项卡上，选择“转到 URL”。 其他部分将显示在此选项的对话框中。  
  
4.  在 **“选择 URL”** 中，键入或选择某一 URL 或者计算结果为某一 URL 的表达式，或者单击下拉箭头并单击包含 URL 的字段的名称。 

    对于发布到配置为本机模式的报表服务器的项，请使用完整路径或相对路径。 例如， `https://<servername>/images/image1.jpg`。 
    
    对于发布到配置为 SharePoint 集成模式的报表服务器的项，请使用完全限定的 URL。 例如， `https://<SharePointservername>/<site>/Documents/images/image1.jpg`。
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="after-you-add-a-hyperlink"></a>添加超链接之后
  
1.  （可选）文本的格式不会自动设置为链接。 对于文本，很有必要更改文本的颜色和效果以指示该文本是一个链接。 例如，在功能区的“主页”选项卡中的 **“字体”** 部分中，将颜色更改为蓝色，并将效果更改为下划线。  
  
7.  若要测试该链接，请单击 **“运行”** 以预览报表，然后单击对其设置此链接的报表项。  
  
## <a name="see-also"></a>另请参阅  
 [交互式排序、文档结构图和链接（报表生成器和 SSRS）](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [创建文档结构图（报表生成器和 SSRS）](../../reporting-services/report-design/create-a-document-map-report-builder-and-ssrs.md)  
  
  
