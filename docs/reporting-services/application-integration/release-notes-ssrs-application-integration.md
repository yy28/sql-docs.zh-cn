---
title: SSRS 报表查看器控件的发行说明
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maggies
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: d6c7130e45e535ad1849bed5713313bf6f89020f
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923809"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>SSRS 的 WebForms 和 WinForms 报表查看器控件的发行说明

这是 WebForms 和 WinForms 的报表查看器控件（与 @no__t [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] （SSRS）相关）的发行说明。

有关 SSRS 的发行说明，请参阅[SQL Server Reporting Services （SSRS）2017及更高版本的发行说明](../release-notes-reporting-services.md)。

## <a name="15013580"></a>150.1358.0
| 更改描述 | 详细信息 |
| :----------------- | :------ |
| Bug 修复 | 还原从项目引用中删除了 Microsoft ReportViewer 设计程序集的更改。 |
|           | 作为其他更改的一部分，两个程序集从15.0 版本更改为15.3。 此已还原。 |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| 更改描述 | 详细信息 |
| :----------------- | :------ |
| Bug 修复  | 适用于高 DPI 监视器的正确打印预览 |
|            | "打印" 对话框将显示在可见空间之外 |
|            | 大量参数导致参数滚动条和下拉列表不能正常工作 |
|            | 修复了包含 Null 和日期时间参数的问题 |
|            | 已将 JQuery 更新到版本3.3。1 |
|            | 修复了 HTML 呈现中与 tablix 单元重叠的情况 |
|            | 删除了设计时项目引用以消除添加到项目的错误 VS 程序集 |
|            | 工具栏的辅助功能修补程序仅为活动项叙述 |
| &nbsp; | &nbsp; |

## <a name="15900148"></a>15.900.148

| 更改描述 | 详细信息 |
| :----------------- | :------ |
| 防止不带参数通过 Server.LoadReportDefinition 加载报表的 bug 修复。  | &nbsp; |
| WebForms 报表查看器控件。 | 支持在 RTL 页面（使用 *direction: rtl;* css 属性更改文本流的页面）中进行嵌入。<br/><br/>支持通过 IReportViewerMessages5  本地化接口自定义打印对话框文本。<br/><br/>改进了辅助功能支持。<br/><br/>&bull; @no__t[为 WebForms 的报表查看器控件](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148)&nbsp; NuGet 包 |
| WinForms 报表查看器控件。 | 应用在高 DPI 模式下运行时进行打印的修补程序。<br/><br/>&bull; @no__t[为 WinForms 的报表查看器控件](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148)&nbsp; NuGet 包 |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>后续步骤

报表查看器控件[入门](integrating-reporting-services-using-reportviewer-controls-get-started.md)。

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)。
