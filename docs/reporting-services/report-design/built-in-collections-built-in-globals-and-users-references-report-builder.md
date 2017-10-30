---
title: "内置的全局和用户引用 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5f5e1149-c967-454d-9a63-18ec4a33d985
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 821c2e768a14af3004971ca8f7b8d8ab76e2c762
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="built-in-collections---built-in-globals-and-users-references-report-builder"></a>内置集合的内置全局和用户引用 （报表生成器）
  内置字段集合包含 **Globals** 和 **User** 集合，表示处理报表时由 Reporting Services 提供的全局值。 **Globals** 集合提供一些值，例如报表名称、开始处理报表的时间，以及报表表头或表尾的当前页码。 **User** 集合提供用户标识符和语言设置。 这些值在表达式中用于对报表中的结果进行筛选。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-globals-collection"></a>使用 Globals 集合  
 **Globals** 集合包含报表的全局变量。 这些变量显示在设计图面上，通过带前缀 （& a) （and 符），例如， `[&ReportName]`。 下表对 **Globals** 集合的成员进行了说明。  
  
|**成员**|**类型**|**Description**|  
|----------------|--------------|---------------------|  
|ExecutionTime|**DateTime**|报表开始运行的日期和时间。|  
|PageNumber|**Integer**|相对于重置页码的分页符的当前页码。 在报表处理开始时，初始值设置为 1。 对于每个呈现的页，该页码将增 1。<br /><br /> 在矩形、 数据区域、 数据区域组或一个代码图，PageBreak 属性中，分页符的页码将 ResetPageNumber 属性设置为**True**。 不支持 Tablix 列层次结构组。<br /><br /> PageNumber 只能用于页眉或页脚中的表达式中。|  
|ReportFolder|**字符串**|包含该报表的文件夹的完整路径。 它不包括报表服务器 URL。|  
|ReportName|**字符串**|报表存储在报表服务器数据库中的名称。|  
|ReportServerUrl|**字符串**|正在运行该报表的报表服务器的 URL。|  
|TotalPages|**Integer**|相对于重置 PageNumber 的分页符的总页数。 如果未设置分页符，则该值与 OverallTotalPages 相同。<br /><br /> TotalPages 只能用于页眉或页脚中的表达式中。|  
|PageName|**字符串**|页的名称。 开始处理报表时，从 InitialPageName（这是一个报表属性）设置初始值。 处理每个报表项时，该值将被来自矩形、数据区域、数据区域组或地图的 PageName 的相应值替换。 不支持 Tablix 列层次结构组。<br /><br /> PageName 只能用于页眉或页脚中的表达式中。|  
|OverallPageNumber|**Integer**|针对整个报表的当前页的页码。 此值不受 ResetPageNumber 影响。<br /><br /> OverallPageNumber 只能用于页眉或页脚中的表达式中。|  
|OverallTotalPages|**Integer**|整个报表的总页数。 此值不受 ResetPageNumber 影响。<br /><br /> OverallTotalPages 只能用于页眉或页脚中的表达式中。|  
|RenderFormat|**RenderFormat**|与当前呈现请求有关的信息。<br /><br /> 有关详细信息，请参阅下一节中的“RenderFormat”。|  
  
 **Globals** 集合的成员将返回一个变量。 如果要在表达式中使用此集合中要求特定数据类型的成员，则必须先转换该变量。 例如，若要将执行时间变量转换为 Date 格式，请使用 `=CDate(Globals!ExecutionTime)`。 有关详细信息，请参阅 [表达式中的数据类型（报表生成器和 SSRS）](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)。  
  
### <a name="renderformat"></a>RenderFormat  
 下表介绍 **RenderFormat**的成员。  
  
|成员|类型|Description|  
|------------|----------|-----------------|  
|名称|**字符串**|呈现器的名称注册在 RSReportServer 配置文件中。<br /><br /> 在报表处理/呈现周期的特定环节可用。|  
|IsInteractive|**Boolean**|当前呈现请求是否使用交互式呈现格式。|  
|DeviceInfo|只读名称/值集合|当前呈现请求的 deviceinfo 参数的键/值对。<br /><br /> 可以通过使用集合中的键或索引指定字符串值。|  
  
### <a name="examples"></a>示例  
 下面的示例演示如何在表达式中使用对 **Globals** 集合的引用：  
  
-   此表达式放置在报表表尾的文本框中，提供了报表的页码和总页数：  
  
     `=Globals.PageNumber & " of " & Globals.TotalPages`  
  
-   此表达式提供了报表的名称和运行时间。 其时间格式为短日期形式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 格式设置字符串：  
  
     `=Globals.ReportName & ", dated " & Format(Globals.ExecutionTime, "d")`  
  
-   此表达式位于所选列的 **“列可见性”** 对话框中，仅当将报表导出到 Excel 后才会显示该列。 否则，此列将会隐藏。  
  
     `EXCELOPENXML` 引用 Office 2007 中包含的 Excel 的格式。 `EXCEL` 引用 Office 2003 中包含的 Excel 的格式。  
  
     `=IIF(Globals!RenderFormat.Name = "EXCELOPENXML" OR Globals!RenderFormat.Name = "EXCEL", false, true)`  
  
## <a name="using-the-user-collection"></a>使用 User 集合  
 **User** 集合包含运行报表的用户的相关数据。 可以使用此集合筛选报表中显示的数据，例如，仅显示当前用户的数据或显示 UserID（如在报表标题中）。 这些变量显示在设计图面上，通过带前缀 （& a) （and 符），例如， `[&UserID]`。  
  
 下表对 **User** 集合的成员进行了说明。  
  
|**成员**|**类型**|**Description**|  
|----------------|--------------|---------------------|  
|**语言**|**字符串**|运行报表的用户的语言。 例如， `en-US`。|  
|**UserID**|**字符串**|运行报表的用户的 ID。 如果您使用的是 Windows 身份验证，则此值为当前用户的域帐户。 此值由 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安全扩展插件确定，此插件可以使用 Windows 身份验证，也可以使用自定义身份验证。|  
  
 有关在报表中支持多种语言的详细信息，请参阅 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SQL Server 联机丛书 [中的](http://go.microsoft.com/fwlink/?LinkId=120955)文档中的“多语言或全局部署的解决方案设计注意事项”。  
  
### <a name="using-locale-settings"></a>使用区域设置  
 可以使用表达式通过 **User.Language** 值来引用客户端计算机上的区域设置，从而确定如何向用户显示报表。 例如，可创建基于区域值而使用不同查询表达式的报表。 查询可以根据返回的语言发生相应更改，从不同的列中检索本地化信息。 您还可以根据此变量在报表或报表项的语言设置中使用表达式。  
  
> [!NOTE]  
>  在更改报表的语言设置时，必须注意由此引发的显示问题。 例如，更改报表的区域设置可以更改报表的日期格式，也可以更改货币格式。 除非已对货币进行转换，否则上述更改可能导致在报表中显示错误的货币符号。 若要避免这种情况，可设置要更改的各个项的语言信息，或将包含货币数据的项设置为特定语言。  
  
### <a name="identifying-userid-for-snapshot-or-history-reports"></a>标识快照或历史记录报表的 UserID  
 在某些情况下，包含 *User!UserID* 变量的报表将无法显示特定于查看报表的当前用户的报表数据。  
  
## <a name="see-also"></a>另请参阅  
 [表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [表达式对话框 &#40;报表生成器 &#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)   
 [表达式 &#40; 中的数据类型报表生成器和 SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [格式设置数字和日期 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [表达式示例 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  

