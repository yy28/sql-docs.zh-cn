---
title: ReportViewer 控件 2016 中的数据收集 | Microsoft Docs
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 68e5a4c9789a6c0485433a3199d8d6a03c2a90d5
ms.sourcegitcommit: a251adad8474b477363df6a121431b837f22bf77
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47864335"
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>使用 ReportViewer 控件集成 Reporting Services - 数据集合

为了更好地了解客户如何使用产品，控件收集匿名使用情况数据。 使用情况数据可使将来开发专注于与客户最相关的改进。

Microsoft SQL Server 和报表查看器的数据收集和用例说明可在[隐私声明](http://go.microsoft.com/fwlink/?LinkID=868444)中找到。

## <a name="opting-out-of-data-collection"></a>选择退出数据收集

可通过 ```EnableTelemetry``` 属性禁用使用情况数据收集。

```
<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
</rsweb:ReportViewer>
```

或在呈现控件之前按实际需要使用。
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>另请参阅

[使用 WebForms 报表查看器控件](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[使用报表查看器控件集成 Reporting Services](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



