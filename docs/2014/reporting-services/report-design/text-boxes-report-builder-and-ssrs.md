---
title: 文本框（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10134"
- sql12.rtp.rptdesigner.textproperties.general.f1
- "10120"
- sql12.rtp.rptdesigner.textboxproperties.general.f1
ms.assetid: df49e4e3-f279-4c63-a03b-b70c095f4ba2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fb96831c54a67a6ea74ca984cb346dcaaf50a335
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104633"
---
# <a name="text-boxes-report-builder-and-ssrs"></a>文本框（报表生成器和 SSRS）
  在您考虑一个文本框时，可能要考虑在类似 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office PowerPoint 的图面上包含文本的独立框。 在报表生成器中，某些文本类似上述文本框，它们可显示标题、说明和标签的文字文本，或者基于表达式显示动态文本。 但表或矩阵（tablix 数据区域）中的每个单元也都包含文本框，可以使用您的报表中独立文本框的格式设置方式来设置这些文本框的格式。  
  
> [!NOTE]  
>  如果将报表数据集字段值直接拖到报表设计图面或报表设计图面上的文本框中，则在运行报表时只能看到结果集中的第一个值。 若要看到某个字段的所有值，必须将该字段拖到表或矩阵内的单元中。 这样，在您运行报表时，将看到该字段中的所有值。  
  
 若要以自由格式布局显示重复的文本，请在列表数据区域中放置一个文本框。 如果想对多个值重复某窗体，例如为每个客户重复一次客户发票窗体，请使用列表。 有关详细信息，请参阅[列出了&#40;报表生成器和 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。  
  
 如果想控制文本框布局和最后一个文本框下面的空白，请使用矩形容器。 有关详细信息，请参阅[矩形和线条（报表生成器和 SSRS）](rectangles-and-lines-report-builder-and-ssrs.md)。  
  
 文本框中的表达式可以包含文字文本、指向数据库中的字段或用来计算数据。 所有表达式都显示为占位符文本，这样您就可以设置数字、颜色以及其他外观属性的格式。 您还可以在同一文本框中将占位符与文字文本合并在一起。  
  
 您可以在任何单个文本框中以多种字体、颜色、样式和操作设置文本格式。 有关详细信息，请参阅 [设置文本和占位符的格式（报表生成器和 SSRS）](formatting-text-and-placeholders-report-builder-and-ssrs.md)的详细信息。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="GrowShrinkTextBox"></a> 扩大和收缩文本框  
 默认情况下，文本框的大小是固定的。 您可以允许文本框基于其内容垂直收缩或扩展。 有关详细信息，请参阅 [允许文本框扩大或收缩（报表生成器和 SSRS）](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)的详细信息。  
  
## <a name="orienting-a-text-box"></a>确定文本框的方向  
 确定文本框的方向可以帮助您创建更具可读性的报表、支持区域设置特定的文本方向、在具有固定页面大小的打印报表中放置更多的列，以及创建具有更吸引人的图形的报表。 文本框可采用不同的方向：水平、垂直或旋转 270 度。 垂直选项最常用于从上到下书写的东亚语言。 在大多数呈现器中，垂直选项处理标志符号旋转属性，以便文本从上到下书写，但字符不在其两侧上。 对于其他语言，在垂直和 270 度选项中，以横向书写文本。  
  
 您可以将方向应用于包含文字文本、来自报表数据集的字段或计算列的文本框。 在报表主体、表或矩阵或者报表页眉和页脚中，文本框可以是独立的。  
  
 下图显示按月对数据进行分组的表报表的三个版本。 包含月份值的文本框使用不同的文本框方向。  
  
 ![rs_TextBoxOrientation](../media/rs-textboxorientation.gif "rs_TextBoxOrientation")  
  
 方向是对文本框设置的并且适用于文本框中的所有文本。 不能为文本框的各个部分指定不同的方向。  
  
 若要快速开始使用更改文本方向，请参阅中关于旋转文本的部分[教程：设置文本格式（报表生成器）](../tutorial-format-text-report-builder.md)。 有关详细信息，请参阅[设置文本框方向&#40;报表生成器和 SSRS&#41;](set-text-box-orientation-report-builder-and-ssrs.md)。  
  
##  <a name="HowTo"></a> 操作指南主题  
 [添加、移动或删除文本框（报表生成器和 SSRS）](add-move-or-delete-a-text-box-report-builder-and-ssrs.md)  
  
 [设置文本框中文本的格式（报表生成器和 SSRS）](format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
 [设置文本框方向（报表生成器和 SSRS）](set-text-box-orientation-report-builder-and-ssrs.md)  
  
 [允许文本框扩大或收缩（报表生成器和 SSRS）](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>请参阅  
 [设置文本和占位符的格式（报表生成器和 SSRS）](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [设置数字和日期格式（报表生成器和 SSRS）](formatting-numbers-and-dates-report-builder-and-ssrs.md)  
  
  
