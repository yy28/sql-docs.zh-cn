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
ms.openlocfilehash: d6d4da6d5574288fa66ea18a9c63b1488a6abcca
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290940"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>WebForms 和 WinForms 的 SSRS 报表查看器控件的发行说明

这些是 WebForms 和 WinForms，与相关的报表查看器控件的发行说明[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS)。

有关 SSRS 的发行说明，请参阅[发行说明的 SQL Server Reporting Services (SSRS) 2017年及更高版本](../release-notes-reporting-services.md)。

## <a name="15900148"></a>15.900.148

| 更改说明 | 详细信息 |
| :----------------- | :------ |
| 防止不带参数通过 Server.LoadReportDefinition 加载报表的 bug 修复。 | &nbsp; |
| WebForms 报表查看器控件。 | 支持在 RTL 页面（使用 *direction: rtl;* css 属性更改文本流的页面）中进行嵌入。<br/><br/>支持通过 IReportViewerMessages5 本地化接口自定义打印对话框文本。<br/><br/>改进了辅助功能支持。<br/><br/>&bull; &nbsp; &nbsp; [报表查看器控件的 WebForms 的 NuGet 包](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| WinForms 报表查看器控件。 | 应用在高 DPI 模式下运行时进行打印的修补程序。<br/><br/>&bull; &nbsp; &nbsp; [报表查看器控件的 WinForms 的 NuGet 包](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>后续步骤

报表查看器控件[入门](integrating-reporting-services-using-reportviewer-controls-get-started.md)。

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)。
