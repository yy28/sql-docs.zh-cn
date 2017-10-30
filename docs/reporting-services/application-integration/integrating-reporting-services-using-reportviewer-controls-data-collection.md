---
title: "ReportViewer 控件 2016年中的数据收集 |Microsoft 文档"
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
caps.latest.revision: 2
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4e8b0226c27380bd2089acf8d2d6c8d7b27c7c5b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>集成 Reporting Services 使用 ReportViewer 控件的数据收集
默认情况下，ReportViewer 控件收集匿名使用信息，以便 Microsoft 能够更好地了解如何使客户使用的控制。 通过创建更好地了解如何部署和使用查看器控件客户，将来开发可以侧重为客户提供最大的价值的改进。

有关 Microsoft SQL Server 2016 版本和其他任何产品及服务的用户数据集收集和使用方式的说明，请参考 [Microsoft 隐私声明](https://www.microsoft.com/EN-US/privacystatement/SQLServer/Default.aspx)。

## <a name="opting-out-of-telemetry"></a>选择退出遥测

可以通过"EnableTelemetry"以编程方式禁用遥测。 这可以通过编辑托管控件的.aspx 页

```
\<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
\</rsweb:ReportViewer>
```

或者，实际地说之前时呈现控件，如与宿主页 Page_Load 调用中一样。
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>另请参阅

[使用 WebForms ReportViewer 控件](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[集成 Reporting Services 使用的 ReportViewer 控件](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 




