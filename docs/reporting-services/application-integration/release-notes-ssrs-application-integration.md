---
title: SSRS 报表查看器控件的发行说明
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maghan
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: 1528358c8aff5d6e99869f0f4f8c1676ee2d5e75
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730904"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>WebForms 和 WinForms 的 SSRS 报表查看器控件的发行说明

这些是 WebForms 和 WinForms，与相关的报表查看器控件的发行说明[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS)。

有关 SSRS 的发行说明，请参阅[发行说明的 SQL Server Reporting Services (SSRS) 2017年及更高版本](../release-notes-reporting-services.md)。

## <a name="15013580"></a>150.1358.0
| 更改说明 | 详细信息 |
| :----------------- | :------ |
| Bug 修复 | 还原 Microsoft.ReportViewer.Design 程序集从引用中删除项目的更改。 |
|           | 作为其他更改的一部分，两个程序集从应为 15.0 版本更改为 15.3。 这已被还原。 |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| 更改说明 | 详细信息 |
| :----------------- | :------ |
| Bug 修复  | 高 DPI 监视器的正确打印预览 |
|            | 打印对话框会显示外部可见的空间 |
|            | 大量的参数会导致参数滚动条和无法正常工作的下拉列表 |
|            | Null 和日期时间参数修复的问题 |
|            | 已更新到版本 3.3.1 JQuery |
|            | 修复了与在 HTML 呈现 tablix 单元格重叠 |
|            | 删除项目引用以消除错误添加到项目的 VS 程序集的设计时 |
|            | 辅助功能修复的工具栏中添加旁白仅为活跃的项目 |
| &nbsp; | &nbsp; |

## <a name="15900148"></a>15.900.148

| 更改说明 | 详细信息 |
| :----------------- | :------ |
| 防止不带参数通过 Server.LoadReportDefinition 加载报表的 bug 修复。  | &nbsp; |
| WebForms 报表查看器控件。 | 支持在 RTL 页面（使用 *direction: rtl;* css 属性更改文本流的页面）中进行嵌入。<br/><br/>支持通过 IReportViewerMessages5  本地化接口自定义打印对话框文本。<br/><br/>改进了辅助功能支持。<br/><br/>&bull; &nbsp; &nbsp; [报表查看器控件的 WebForms 的 NuGet 包](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| WinForms 报表查看器控件。 | 应用在高 DPI 模式下运行时进行打印的修补程序。<br/><br/>&bull; &nbsp; &nbsp; [报表查看器控件的 WinForms 的 NuGet 包](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>后续步骤

报表查看器控件[入门](integrating-reporting-services-using-reportviewer-controls-get-started.md)。

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)。
