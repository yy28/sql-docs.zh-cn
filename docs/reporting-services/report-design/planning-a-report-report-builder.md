---
title: 规划报表（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- getting started
- report design
ms.assetid: 79113505-1ce8-4f8c-9260-d861838f7813
caps.latest.revision: 19
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 84f5898fcc0bf443440a6dcfd3bc88551534e8a5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33025114"
---
# <a name="planning-a-report-report-builder"></a>规划报表 (报表生成器)
  利用报表生成器可创建多种类型的分页报表。 例如，可以创建显示摘要或详细销售数据、营销和销售趋势的报表、操作报表或面板。 还可以为销售订单、产品目录或套用信函等创建利用丰富格式文本的报表。 所有这些报表都是在报表生成器中使用相同基本构造块的不同组合创建的。 若要创建有用且易于理解的报表，报表生成器可帮助首先进行规划。 开始创建报表之前最好考虑以下几个问题：  
  
-   **要以何种格式显示报表？**  
  
     可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] web 门户等浏览器中联机呈现报表，也可以将它们导出为 Excel、Word 或 PDF 等其他格式。 报表采用的最终格式是需要考虑的重要因素，因为并非所有功能在所有导出格式中都可用。 有关详细信息，请参阅 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)中用于控制分页的规则。  
  
-   **希望在报表中用何种结构来呈现数据？**  
  
     您可以选择表格、矩阵（类似于交叉表或数据透视表）、图表、自由格式结构或以上几种结构的任意组合来呈现数据。 有关详细信息，请参阅[表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)和[图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)。  
  
-   **希望使用什么样的报表外观？**  
  
     报表生成器提供了许多报表项，您可以将其添加到报表中以使报表更易于阅读、突出显示关键信息、帮助用户导航报表等。 了解要如何显示报表才能确定是否需要文本框、矩形、图像和线条等报表项。 您还可能希望显示或隐藏项，添加文档结构图（包括钻取报表或子报表），或者链接到其他报表。 有关详细信息，请参阅[图像、文本框、矩形和线条（报表生成器和 SSRS）](../../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)和[交互式排序、文档结构图和链接（报表生成器和 SSRS）](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)。  
  
-   **希望读者看到哪些数据？是否应针对不同用户筛选数据或格式？**  
  
     您可能希望将报表范围缩小到特定用户或位置，或者缩小到特定时间段。 若要筛选报表数据，请使用参数来检索并只显示所需的数据。 有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)的详细信息。  
  
-   **是否需要创建自己的计算？**  
  
     有时，数据源和数据集不包含报表需要的确切字段。 在这种情况下，您可能需要创建自己的计算字段。 例如，您可能要以单价乘以数量来获得行项的销售金额。 表达式还用于提供条件格式和其他高级功能。 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)。  
  
-   **最初是否要隐藏报表项？**  
  
     首次运行报表时，可考虑是否要隐藏报表项（包括数据区域、组和列）。 例如，最初可以呈现摘要表，然后深化到详细数据。 有关详细信息，请参阅[深化操作（报表生成器和 SSRS）](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)。  
  
-   **打算如何传递报表？**  
  
     您可以将报表保存到本地计算机，并继续在本地使用它或运行它，供自己参考。 但是，若要与其他人共享报表，需要将报表保存到配置为本机模式的报表服务器或 SharePoint 集成模式下的报表服务器。 将报表保存到服务器可允许其他人在需要时运行报表。 另外，报表服务器管理员可以设置对报表的订阅，或者设置通过电子邮件向他人传递报表。 您可以根据需要以特定导出格式传递报表。 有关详细信息，请参阅 [查找、查看和管理报表（报表生成器和 SSRS）](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2016 中的报表生成器](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [报表创作概念（报表生成器和 SSRS）](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [报表生成器教程](../../reporting-services/report-builder-tutorials.md)  
  
  
