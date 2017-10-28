---
title: "排查 Reporting Services 报表呈现问题 |Microsoft 文档"
ms.custom: 
ms.date: 02/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1e0fb399-4c16-438a-92cb-db3e877896d0
caps.latest.revision: 4
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 91629c6d86f1616b19026cbc0e670fff51553dda
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot-reporting-services-report-rendering-issues"></a>排查 Reporting Services 报表呈现问题
将报表数据与布局信息组合起来后，会将组合的报表发送到报表呈现器。 例如，本地预览报表时，您是使用 HTML 呈现器查看组合报表。 使用本主题可帮助解决特定于报表呈现的问题。   
  
## <a name="why-do-i-have-extra-white-space-including-blank-pages-in-my-report"></a>为什么报表中有额外的空白区域和空白页？  
在报表处理过程中会自动调整报表项，以保留定义为报表一部分的空白区域。 会保留报表设计视图中的空白区域。 在报表设计图面上，白色背景表示查看、导出或打印报表时保留的空白区域，具体取决于目标介质。  
  
### <a name="white-space-and-page-breaks-interact-during-rendering"></a>呈现过程中，空白区域和分页符会互相影响  
查看报表或将报表导出为某种文件格式时，关联的呈现扩展插件会处理报表，并将其保存为指定文件格式。 每种呈现扩展插件都会根据特定规则处理报表中的空白区域。 空白区域还受以下因素影响：页面设置属性、对报表项设置的分页符、表体中放置的报表项的相对位置、某些报表项的 KeepTogether 属性以及报表项是否位于父容器中。   
  
若要消除报表宽度导致的额外页，请拖动报表设计图面的边缘使其与最外面的报表项对齐。 对于从左到右的报表布局，请拖动要与最外面的报表项对齐的右边缘。 有关详细信息，请参阅 [呈现行为](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
### <a name="white-space-is-not-preserved-at-the-end-of-a-report"></a>在报表末尾没有保留空白区域  
Reporting Services 提供了一个选项，可用来控制是保留还是消除报表末尾的空白区域。   
  
若要保留报表末尾的空白区域，请选择报表，在“属性”窗格中滚动到 ConsumeContainerWhitespace，然后键入 False。   
  
## <a name="why-do-my-reports-look-different-when-exported-to-different-formats"></a>为什么在将报表导出为不同格式时，报表看起来有所不同？  
运行报表后，可以将其导出为其他格式，例如 Excel、Word 或 PDF。 根据导出报表的格式，某些规则和限制可能适用。 在创建报表时，可以考虑这些来解决许多限制。 在报表中可能需要使用稍有不同的布局，仔细对齐报表中的项，将报表表尾限制为单行文本等。 还可以通过 RenderFormat 内置全局，针对不同呈现器使用不同的报表布局。 其他内置全局可帮助您管理导出格式中的分页和为 Excel 中的工作表选项卡命名。 有关详细信息，请参阅 [导出报表](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) 和 [使用用户引用的内置全局](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)。  
  
## <a name="how-can-i-view-all-my-report-data-on-one-page"></a>如何在一页上查看所有报表数据？  
对于没有大量数据的报表，若要获得交互查看体验，可能需要在一页上查看所有数据。   
  
对于软分页呈现器，若要在一页上查看所有数据，请在“报表”属性中将 InteractiveHeight 设置为 0。 在软分页呈现器中将忽略现有分页符。   
  
> [!NOTE]  
> 如果报表没有分页符，则必须先处理整个报表，才能查看第一页。   
  
有关呈现器类别的详细信息，请参阅 [渲染行为](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
## <a name="reports-do-not-run-when-your-browser-is-configured-to-prompt-for-credentials"></a>当浏览器配置为提示输入凭据时，报表不运行  
当将浏览器配置为提示输入凭据且将数据源配置为使用集成 Windows 身份验证时，查看报表时可能会失败，且显示一条错误消息。 当数据源位于与报表服务器不同的计算机上，数据源配置为使用 Windows 身份验证且浏览器设置为提示输入凭据时，会出现这种情况。 下面是您将看到的消息的示例。  
  
如果将数据源配置为 Microsoft SQL Server 连接类型：  
`An error has occurred during report processing.`  
`Cannot create a connection to data source 'localhost'.`  
`Login failed for user '(null)'. Reason: Not associated with a trusted SQL Server connection.`  
  
如果数据源配置为 Microsoft SharePoint 列表连接类型：  
`An error occurred during client rendering.`   
`An error has occurred during report processing.`   
`Query execution failed for dataset 'DataSet1'.`   
`The request failed with HTTP status 401: Unauthorized.`  
  
**此问题的解决办法：** 将数据源修改为使用存储的凭据，而不是 Windows 凭据。  
  
**此问题适用于：** 配置为提示输入凭据的浏览器。  
  
## <a name="see-also"></a>另请参阅  
[错误和事件 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Reporting Services 报表的数据检索问题疑难解答](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Reporting Services 订阅和传递的疑难解答](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]


