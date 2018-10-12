---
title: Reporting Services 报表查看器控件的更改日志
ms.date: 09/19/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: 57eca1ced359ec08dc9b64f6840d0eadf1fb3f3e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771375"
---
# <a name="changelog-for-the-report-viewer-controls"></a>报表查看器控件的更改日志

此更改日志跟踪 WinForms 和 WebForms 报表查看器控件的版本。

## <a name="15900148"></a>15.900.148
利用此更新
 - 防止不带参数通过 Server.LoadReportDefinition 加载报表的 bug 修复

[WebForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) 报表查看器控件
 - 支持在 RTL 页面（使用 *direction: rtl;* css 属性更改文本流的页面）中进行嵌入。
 - 支持通过 IReportViewerMessages5 本地化接口自定义打印对话框文本。
 - 改进了辅助功能支持。

[WinForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) 报表查看器控件
 - 应用在高 DPI 模式下运行时进行打印的修补程序。

## <a name="next-steps"></a>后续步骤

报表查看器控件[入门](integrating-reporting-services-using-reportviewer-controls-get-started.md)  
更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
