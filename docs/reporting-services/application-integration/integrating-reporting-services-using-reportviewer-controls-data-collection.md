---
title: ReportViewer 控件 2016 中的数据收集
uthor: markingmyname
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.custom: ''
ms.date: 09/18/2018
ms.openlocfilehash: 747c073907158e16a16dc8acd7f36ec457e32e80
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68256097"
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>使用 ReportViewer 控件集成 Reporting Services - 数据集合

为了更好地了解客户如何使用产品，控件收集匿名使用情况数据。 使用情况数据可使将来开发专注于与客户最相关的改进。

Microsoft SQL Server 和报表查看器的数据收集和用例说明可在[隐私声明](https://go.microsoft.com/fwlink/?LinkID=868444)中找到。

## <a name="opting-out-of-data-collection"></a>选择退出数据收集

可通过 ```EnableTelemetry``` 属性禁用使用情况数据收集。

```xml
<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
</rsweb:ReportViewer>
```

或在呈现控件之前按实际需要使用。
    
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>另请参阅

[使用 WebForms 报表查看器控件](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[使用报表查看器控件集成 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



