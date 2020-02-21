---
title: 报表设计视图（报表生成器）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- "10440"
- "10426"
- "10439"
- "10434"
- "10438"
- "10436"
helpviewer_keywords:
- reports, creating
- user interface
- overview of Report Builder
ms.assetid: 1544472c-2803-448d-af52-e901cb457a00
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7ecc2115b106fe61492be388c90cfa2bd27eae9f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "74190035"
---
# <a name="report-design-view-report-builder"></a>报表设计视图（报表生成器）
  报表生成器窗口旨在帮助轻松组织报表资源并快速生成所需分页报表。 设计图面位于窗口中心，周围是功能区和窗格。 设计图面用于添加和组织报表项。 本文说明用于添加、选择和组织报表资源，以及更改报表项属性的窗格。  
  
 ![报表生成器设计视图](../../reporting-services/report-builder/media/ssrb-designview.png "报表生成器设计视图")  
  
1.  功能区  
  
2.  [“参数”窗格](#Ribbon)  
  
3.  [报表部件库](#ReptPartGallery)  
  
4.  [属性窗格](#PropertiesPane)  
  
5.  [报表设计图面](#RptDesignSurface)  
  
6.  [“报表数据”窗格](#ReptDataPane)  
  
7.  [“分组”窗格](#GroupPane)  
  
8.  当前报表状态栏  
  
##  <a name="Ribbon"></a> “参数”窗格  
 通过报表参数，可以控制报表数据、将相关报表连接在一起以及更改报表显示。 “参数”窗格中为报表参数提供灵活的布局。  
  
 阅读有关 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)的详细信息。  
  
  
##  <a name="RptDesignSurface"></a> 报表设计图面  
 报表生成器的报表设计图面是用于设计报表的主工作区。 若要将报表项（如数据区域、子报表、文本框、图像、矩形和线条）放入报表中，请从功能区或报表部件库将它们添加到设计图面。 在设计图面中，您可以向报表项添加组、表达式、参数、筛选器、操作、可见性和格式设置。  
  
 还可以更改以下项：  
  
-   表体属性（如边框和填充颜色），方法是右键单击设计图面上所有报表项以外的白色区域，再单击“表体属性”  。  
  
-   表头和表尾属性（如边框和填充颜色），方法是右键单击设计图面上表头和表尾区域中所有报表项以外的白色区域，再单击“表头属性”或“表尾属性”   。  
  
-   报表自身的属性（如页面设置），方法是右键单击设计图面周围的蓝色区域，再单击“报表属性”  。  
  
-   报表项的属性，方法是右键单击它们，再单击“属性”  。  
  
 有关使用键盘操作设计图面上的项的信息，请参阅[键盘快捷方式（报表生成器）](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
  
### <a name="design-surface-size-and-print-area"></a>设计图面大小和打印区域  
 设计图面大小可能与您指定用来打印报表的打印区域的页面大小不同。 更改设计图面的大小将不会更改报表的打印区域。 不论您为报表的打印区域设置何种大小，整个设计区域的大小都不会改变。 有关详细信息，请参阅[呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
> [!TIP]  
>  若要显示标尺，请在“视图”  选项卡上，选中“标尺”  复选框。  
  
  
##  <a name="ReptDataPane"></a> The Report Data Pane  
 在“报表数据”窗格中，在设计报表布局前可以定义报表所需的报表数据和报表资源。 例如，您可以向“报表数据”窗格中添加数据源、数据集、计算字段、报表参数和图像。  
  
 在将项添加到“报表数据”窗格中后，将字段拖到报表设计图面上的报表项，就可以控制数据在报表中的显示位置。  
  
> [!TIP]  
>  如果将某个字段从“报表数据”窗格直接拖到报表设计图面，而不是将其放在数据区域（如表或图表）中，则在运行报表时只能看到该字段中数据的第一个值。  
  
 还可以将内置字段从“报表数据”窗格中拖到报表设计图面中。 呈现时，这些字段提供有关报表的信息，例如报表名称、报表中的总页数以及当前页码。  
  
 在您向报表设计图面中添加某些项时，这些项也会自动添加到“报表数据”窗格中。 例如，如果您从“报表部件库”添加一个报表部件，该报表部件是一个数据区域，则数据集会自动添加到“报表数据”窗格中。 有关详细信息，请参阅 [报表生成器中的报表部件和数据集](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)。 另外，如果您在报表中嵌入一个图像，则该图像将添加到“报表数据”窗格的“图像”文件夹中。  
  
> [!NOTE]  
>  您可以使用 **“新建”** 按钮向“报表数据”窗格添加新项。 您可以从同一数据源或其他数据源向报表添加多个数据集。 可以从报表服务器添加共享数据集。 若要从同一数据源添加新数据集，请右键单击某个数据源，然后单击“添加数据集”  。  
  
 有关“报表数据”窗格中各项的详细信息，请参阅以下主题：  
  
-   [内置的全局和用户引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)  
  
-   [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [图像（报表生成器和 SSRS）](../../reporting-services/report-design/images-report-builder-and-ssrs.md)  
  
-   [创建数据连接字符串 - 报表生成器和 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
-   [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
-   [数据集字段集合（报表生成器和 SSRS）](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
##  <a name="ReptPartGallery"></a> 报表部件库  
 创建报表的最简单方式是在该报表服务器或集成到 SharePoint 站点的报表服务器上查找现有报表部件（如表或图表）。  
  
 单击“插入”选项卡上的“报表部件”打开报表部件库  。 可以在曲终搜索要添加到报表中的报表部件。 可以按照报表部件的全名或部分名称、创建者、最后修改者、最后修改时间、存储位置以及报表部件的类型，对报表部件进行筛选。 例如，您可以搜索由您的同事之一在上周创建的所有图表。  
  
> [!NOTE]  
>  要查看报表部件库，需要连接到服务器。  
  
 您可以采用缩略图或列表的形式查看搜索结果，并且可以按名称、创建日期和修改日期以及创建者对搜索结果进行排序。 有关详细信息，请参阅[报表部件（报表生成器和 SSRS）](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)。  
  
  
##  <a name="PropertiesPane"></a> “属性”窗格（报表生成器）  
 报表中的每一项（包括数据区域、图像、文本框和表体本身）都有相关联的属性。 例如，文本框的 BorderColor 属性指示文本框的边框颜色值，报表的 PageSize 属性指示报表的页大小。  
  
 这些属性显示在“属性”窗格中。 该窗格中的属性会根据所选择的报表项发生变化。  
  
 若要看到“属性”窗格，请在“视图”选项卡的“显示/隐藏”组中单击“属性”。  
  
### <a name="changing-property-values"></a>更改属性值  
 在报表生成器中，可通过多种方式来更改报表项的属性：  
  
-   单击功能区上的按钮和列表。  
  
-   在对话框内更改设置。  
  
-   在“属性”窗格内更改属性值。  
  
 可以在对话框和功能区上找到最常用的属性。  
  
 根据相应的属性，可以从下拉列表中设置属性值、键入值或单击 `<Expression>` 来创建表达式。  
  
### <a name="changing-the-properties-pane-view"></a>更改“属性”窗格视图  
 默认情况下，“属性”窗格中显示的属性是按大的类别（例如操作、边框、填充、字体和常规）分类的。 每个类别都有一组与其相关联的属性。 例如，在“字体”类别中列出以下属性：Color、FontFamily、FontSize、FontStyle、FontWeight、LineHeight 和 TextDecoration。 如果愿意，可以按字母顺序排列该窗格内列出的所有属性。 这会删除类别并按字母顺序列出所有属性，而不考虑类别。  
  
 “属性”窗格的顶部有三个按钮：“类别”、“按字母顺序排序”和“属性页”。 单击“按分类顺序”和“按字母顺序”按钮可在“属性”窗格视图之间切换。 单击 **“属性页”** 按钮可打开所选报表项的属性对话框。  
  
  
##  <a name="GroupPane"></a> “分组”窗格 (Report Builder)  
 使用组可以将报表数据组织成可视层次结构，也可以计算总计。 可以在设计图面上或“分组”窗格中查看数据区域内的行组和列组。 “分组”窗格有两个窗格：“行组”和“列组”。 在你选择数据区域后，“分组”窗格会将此数据区域内的所有组显示为一个层次结构列表：子组以缩进的方式显示在其父组下方。  
  
 ![报表生成器行组](../../reporting-services/report-builder/media/ssrb-rowgroups.png "报表生成器行组")  
  
 可通过将字段从“报表数据”窗格中拖放到设计图面上或“分组”窗格中来创建组。 在“分组”窗格中，可以添加父组、相邻组和子组，更改组属性以及删除组。  
  
 默认情况下会显示“分组”窗格，但可以通过在“视图”选项卡上清除“分组窗格”复选框来关闭该窗格。“分组”窗格对“图表”或“仪表”数据区域不可用。  
  
 有关详细信息，请参阅[“分组”窗格（报表生成器）](../../reporting-services/report-design/grouping-pane-report-builder.md)和[了解组（报表生成器和 SSRS）](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)。  
  
  
##  <a name="RunMode"></a> 在运行模式下预览报表  
 在报表设计视图中，您没有使用实际数据，而是使用由字段名称或表达式表示的数据表示形式。 如果要查看在您所设计的报表上下文中显示的实际数据，可以运行该报表以预览报表布局中显示的基础数据库中的数据。 通过在报表的设计和运行之间切换，您可以调整报表的设计并立即查看结果。 若要预览报表，请单击功能区上 **“视图”** 组中的 **“运行”** group on the ribbon.  
  
 单击 **“运行”** 时，报表生成器将连接到报表数据源、在您的计算机上缓存数据、组合数据和布局，然后在 HTML 查看器中呈现报表。 在继续设计报表时可以任意多次运行报表。 对报表满意后，可以将报表保存到报表服务器，在该服务器上具有相应权限的其他人可以查看该报表。  
   
 阅读有关 [在报表生成器中预览报表](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)的详细信息。  
  
### <a name="running-a-report-with-parameters"></a>使用参数运行报表  
 当您运行报表时，该报表会自动进行处理。 如果报表中包含参数，则只有在所有参数都具有默认值的情况下，该报表才能自动运行。 如果某个参数没有默认值，当运行报表时，需要为参数选择一个值，然后在“运行”选项卡上单击 **“查看报表”** 。有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)的详细信息。  
  
### <a name="print-preview"></a>打印预览  
 在“运行”模式下预览报表时，报表像是以 HTML 格式生成的报表。 虽然预览并非 HTML 格式，但报表的布局和分页与 HTML 格式的输出结果类似。 可通过切换到打印预览模式，查看报表的打印效果。 单击 **“运行”** 选项卡上的 **“打印预览”** 按钮。所显示的报表就如同打印在纸张上一样。 此视图与图像呈现扩展插件和 PDF 呈现扩展插件所生成的输出类似。 虽然打印预览并非图像或 PDF 文件，但报表的布局和分页与这些格式的输出类似。  
  
  
## <a name="see-also"></a>另请参阅  
 [查找、查看和管理报表（报表生成器和 SSRS）](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [SQL Server 中的报表生成器](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  
  
