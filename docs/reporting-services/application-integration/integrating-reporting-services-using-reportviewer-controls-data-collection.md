---
title: ReportViewer 控件 2016 中的数据收集 | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: application-integration
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
caps.latest.revision: 2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: bc1edeb74cced8b18275b57deca6b078c13a56d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33013754"
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>使用 ReportViewer 控件集成 Reporting Services - 数据集合
默认情况下，ReportViewer 控件会收集匿名使用情况信息，以便 Microsoft 更好地了解客户如何使用该控件。 通过更好地了解客户如何部署和使用查看器控件，未来的开发可以专注改进，为客户提供最大的价值。

有关 Microsoft SQL Server 2016 版本和其他任何产品及服务的用户数据集收集和使用方式的说明，请参考 [Microsoft 隐私声明](https://www.microsoft.com/EN-US/privacystatement/SQLServer/Default.aspx)。

## <a name="opting-out-of-telemetry"></a>选择退出遥测

可通过“EnableTelemetry”以编程方式禁用遥测。 通过编辑托管控件的 .aspx 页面可完成此操作

```
\<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
\</rsweb:ReportViewer>
```

或者，如果讲求实效，可以在呈现控件之前，例如在托管页面的 Page_Load 调用中完成此操作。
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>另请参阅

[使用 WebForms ReportViewer 控件](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[使用 ReportViewer 控件集成 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



