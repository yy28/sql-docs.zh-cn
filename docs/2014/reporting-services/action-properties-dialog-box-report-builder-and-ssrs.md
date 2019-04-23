---
title: 操作属性对话框 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shared.action.f1
- "10413"
- "10504"
- sql12.rtp.rptdesigner.calculatedseriesproperties.action.f1
- sql12.rtp.rptdesigner.pictureproperties.action.f1
- sql12.rtp.rptdesigner.actionproperties.f1
- sql12.rtp.rptdesigner.charttitleproperties.action.f1
- "10133"
- "10052"
- "10147"
- sql12.rtp.rptdesigner.chartproperties.action.f1
- "10122"
- sql12.rtp.rptdesigner.serieslabelproperties.action.f1
- sql12.rtp.rptdesigner.textboxproperties.action.f1
- "10162"
- "10168"
- sql12.rtp.rptdesigner.textproperties.action.f1
- sql12.rtp.rptdesigner.placeholderproperties.action.f1
- "10250"
- "10129"
- "10244"
- sql12.rtp.rptdesigner.seriesproperties.action.f1
ms.assetid: 2c5d915b-4f97-42cf-b8f1-49ca3ff3d0f9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 125b40193edca5dc60fa86fe5818f7722f5af91c
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59956823"
---
# <a name="action-properties-dialog-box-report-builder-and-ssrs"></a>“操作属性”对话框（报表生成器和 SSRS）
  使用 **“操作”** 对话框可以为支持链接的图表、仪表和地图元素启用超链接选项。 定义一项操作，以便用户单击报表并链接到 URL、同一报表服务器或与报表服务器集成的 SharePoint 站点上的其他报表，或链接到同一报表中的其他位置。  
  
## <a name="options"></a>选项  
 **启用为操作**  
 选择一个选项，指示在用户单击该项时将执行的操作。  
  
 **无**  
 选择此选项可指示该项没有任何操作。  
  
 **转到报表**  
 选择此选项可以创建指向位于报表服务器上的钻取报表的链接。 选择 **“转到报表”** 时，页面上将显示以下其他选项。  
  
 **指定报表**  
 键入或选择要用作钻取报表的报表的名称。 钻取报表必须与此报表位于同一报表服务器上。  
  
 对于发布到配置为本机模式的报表服务器的报表，请使用不带文件扩展名的完整路径或相对路径。 如果该报表与当前报表位于同一文件夹中，则只需使用该报表的名称即可。 如果报表位于同一报表服务器上的其他文件夹中，则使用相对路径或完整路径。 相对路径从当前文件夹开始并且在文件夹层次结构中上移，例如 ../Folder2/Report1。 完整路径从 /（即主文件夹）开始。 例如，/Reports/Report1。  
  
 对于发布到配置为 SharePoint 集成模式的报表服务器的报表，请使用带有文件扩展名 (.rdl) 的完全限定 URL。 例如， http://*\<SharePointservername > /\<站点 >*/Documents/Report1.rdl。 不支持相对路径。  
  
 有关详细信息，请参阅 msdn.microsoft.com 上[报表生成器文档](https://go.microsoft.com/fwlink/?LinkId=154494)中的[指定外部项的路径（报表生成器和 SSRS）](report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
 **使用这些参数运行报表**  
 添加要传递给钻取报表的参数列表。 参数名称必须与为目标报表定义的参数相匹配。 使用 **“添加”** 和 **“删除”** 按钮可添加和删除参数，使用向上键和向下键可对参数列表进行排序。  
  
 **“添加”**  
 添加要传递给钻取报表的新参数。  
  
 **删除**  
 删除钻取报表的参数。  
  
 **向上键**  
 在列表中向上移动参数。  
  
 **向下键**  
 在列表中向下移动参数。  
  
 **名称**  
 键入表示钻取报表中所定义参数的名称的文本。  
  
 **ReplTest1**  
 键入或选择要传递给钻取报表中的命名参数的值。 单击“表达式” (*fx*) 按钮可编辑表达式。  
  
 **Omit**  
 选择此选项可阻止参数运行。 默认情况下，此复选框已清除，处于不活动状态。 若要选中该复选框，请单击“表达式”(fx) 按钮，再键入 **True** 或创建表达式。 当单击 **“表达式”** 对话框中的 **“确定”** 时，即会选中此复选框。  
  
 **转到书签**  
 选择此选项可以定义指向当前报表内书签的链接。 选择 **“转到书签”** 时，页面上将显示以下其他选项。  
  
 **选择书签**  
 键入或选择用户单击该链接时，将跳至的报表书签 ID。 单击“表达式”(fx) 按钮，更改表达式。 书签 ID 可以是静态 ID，也可以是计算结果为书签 ID 的表达式。 表达式中可以包括含有书签 ID 的字段。  
  
 若要链接到书签，首先必须设置报表项的“书签”属性。 若要设置“书签”属性，请选择一个报表项并在“属性”窗格中键入书签 ID 的值或表达式；例如，SalesChart 或 5TopSales。  
  
 **转到 URL**  
 选择此选项可以定义指向网页的链接。 键入或选择网页的 URL 或计算结果为网页的 URL 的表达式。 单击“表达式”(fx) 按钮，更改表达式。 此表达式可以有一个包含 URL 的字段。 选择 **“转到 URL”** 时，页面上将显示以下其他选项。  
  
 **选择 URL**  
 键入或输入相应项的 URL。 对于发布到配置为本机模式的报表服务器的项，请使用完整路径或相对路径。 例如， http://*\<服务器名 >*/images/image1.jpg。 对于发布到 SharePoint 集成模式下配置的报表服务器的项，请使用完全限定的 URL (例如 http://*\<SharePointservername > /\<站点 >*  /记录/映像 /image1.jpg)。  
  
## <a name="see-also"></a>请参阅  
 [图表（报表生成器和 SSRS）](report-design/charts-report-builder-and-ssrs.md)   
 [用于对话框、窗格和向导的报表生成器帮助](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [报表参数（报表生成器和报表设计器）](report-design/report-parameters-report-builder-and-report-designer.md)   
 [添加子报表和参数（报表生成器和 SSRS）](report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [交互式排序、文档结构图和链接（报表生成器和 SSRS）](report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)  
  
  
