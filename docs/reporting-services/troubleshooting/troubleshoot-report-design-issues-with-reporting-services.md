---
title: 解决 Reporting Services 报表设计问题 | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: a0d103da-5a3e-475c-a71a-9e23476095e2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3eb298bc6b359b0df92566f9add8d7011cdc907
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "65573844"
---
# <a name="troubleshoot-report-design-issues-with-reporting-services"></a>解决 Reporting Services 报表设计问题
在报表创作应用程序的设计视图中创建报表布局时，可能发生报表设计问题。 使用本主题可以帮助解决这些问题。   
  
## <a name="why-does-my-text-box-show-only-a-single-value-and-not-repeat-for-every-row"></a>为什么文本框仅显示一个值，并且不是每行都重复？  
文本框中数据集字段引用仅呈现一次，并显示数据集中的第一个值。   
  
**文本框父级是表体**  
  
  
直接添加到设计图面的文本框只能显示数据集的聚合值。  
  
若要验证文本框的父容器，请选择文本框，在“属性”窗格中滚动到 **“父级”** 。   
  
如果需要显示数据集中每个值的文本框，请使用数据区域，例如表或矩阵。 默认情况下，表或矩阵中的每个单元格都包含一个文本框。 将数据集字段拖到每个单元格中。   
  
## <a name="why-cant-i-add-total-pages-to-my-report"></a>为什么无法向报表中添加总页数？  
内置字段 `[&PageNumber]` 和 `[&TotalPages]` 在报表正文中无效。   
  
PageNumber 和 TotalPages 仅在页眉和页脚中有效。  
  
  
内置字段 [&PageNumber] 和 [&TotalPages] 仅在页眉和页脚中有效。   
  
若要向报表中添加 [&PageNumber] 或 [&TotalPages]，必须首先添加页眉或页脚。 有关详细信息，请参阅 [添加或删除页眉](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
> 在页眉或页脚中包含 [&TotalPages] 可能会对报表处理有影响。 有关详细信息，请参阅“报表故障排除：以特定文件格式导出的报表”。  
[排除 Reporting Services 报表处理故障](../../reporting-services/troubleshooting/troubleshoot-processing-of-reporting-services-reports.md)。  
  
## <a name="how-do-i-design-two-tables-or-a-chart-and-a-table-to-display-side-by-side"></a>如何设计并排显示的两个表或一个图表和一个表？  
设计报表不是一种 WYSISYG（“所见即所得”）体验。 报表处理器会将数据、报表项、报表布局信息（如空白区域）、容器和表达式组合起来以生成已编译报表，然后将报表传递给报表呈现器，对报表进行“布局”以获得指定的查看体验：作为 HTML 浏览器进行交互或作为一种文件格式。 自动布局算法可以生成您可能需要更改的报表布局。   
  
### <a name="rendering-rules-use-page-size-containers-peer-objects-relative-placement-and-white-space-to-determine-layout"></a>呈现规则使用页面大小、容器、对等对象、相对位置和空白区域以确定布局  
通常，报表会增大以容纳数据，将忽略其他报表项。   
  
若要将多个数据区域或报表项分组到一起，请将它们放在同一父容器中。 例如，将图表和表放在一个矩形容器中，将它们沿上边缘对齐以便并排显示。 有关详细信息，请参阅 [报表生成器中的呈现行为](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
[排查与 Reporting Services 报表相关的数据检索问题](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Reporting Services 订阅和传递的疑难解答](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

