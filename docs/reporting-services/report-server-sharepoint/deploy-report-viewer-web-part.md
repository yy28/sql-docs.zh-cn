---
title: "部署报表查看器 web 部件在 SharePoint 站点上的 |Microsoft 文档"
ms.custom: 
ms.date: 09/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a9397f427cac18d0c8bfc663f6bd477b0440b8a3
ms.openlocfilehash: ed93b0fd5161686becb4cca05c005fd281f2c176
ms.contentlocale: zh-cn
ms.lasthandoff: 09/15/2017

---

# <a name="deploy-the-report-viewer-web-part-on-a-sharepoint-site"></a>部署 SharePoint 站点上的报表查看器 web 部件

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

报表查看器 Web 部件是自定义 Web 部件，可以用于在 SharePoint 站点内查看 SQL Server Reporting Services （本机模式） 报表。 可以使用 Web 部件查看、 导航、 打印和导出的报表服务器上的报表。 报表查看器 Web 部件都与 SQL Server Reporting Services 报表服务器或 Power BI 报表服务器处理的报表定义 (.rdl) 文件关联。 此报表查看器 web 部件不能与托管在 Power BI 报表服务器中的 Power BI 报表中使用。

使用以下说明手动部署报表查看器 web 部件添加到 SharePoint Server 2013 或 SharePoint Server 2016 环境解决方案包。 部署解决方案是配置 web 部件所需的步骤。

**报表查看器 web 部件是独立解决方案包，并且不是与用于 SQL Server Reporting Services SharePoint 集成模式相关联。**

## <a name="requirements"></a>要求

**支持的操作系统：**  
* Windows Server 2008 R2 SP1 和更高版本

**支持 SharePoint Server 版本：**  
* SharePoint Server 2016
* SharePoint Server 2013

**支持 Reporting Services 版本：**  
* SQL Server 2008 Reporting Services （本机模式） 和更高版本。
* Power BI 报表服务器

## <a name="download-the-report-viewer-web-part-solution-package"></a>下载报表查看器 web 部件解决方案包

报表查看器 web 部件在 Microsoft 下载中心才可用。

[下载报表查看器 web 部件解决方案包](https://www.microsoft.com/en-us/download/details.aspx?id=55949)

## <a name="deploy-the-farm-solution"></a>部署场解决方案

本部分演示如何将解决方案包部署到你的 SharePoint 场。 此任务仅需执行一次。

1. 在 SharePoint 服务器上，打开 SharePoint Management Shell 使用**以管理员身份运行**选项。

2. 运行[Add-spsolution](https://technet.microsoft.com/library/ff607552(v=office.16).aspx)添加场解决方案。

    ```
    Add-SPSolution –LiteralPath "{path to file}\ReportViewerWebPart.wsp"
    ```

    该 cmdlet 返回解决方案的名称、其解决方案 ID 和 Deployed=False。 在下一步骤中，您将部署解决方案。

3. 运行[Install-spsolution](https://technet.microsoft.com/library/ff607534(v=office.16).aspx) cmdlet 以便部署场解决方案。

    **SharePoint 2013**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -CompatibilityLevel "14,15" -GACDeployment -WebApplication {URL to web application}
    ```

    **SharePoint 2016**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -GACDeployment -WebApplication {URL to web application}
    ```

## <a name="activate-feature"></a>激活功能

1. 在 SharePoint 网站上，选择**齿轮**图标在左上角，选择 **站点设置*。

    ![从齿轮图标的站点设置。](media/sharepoint-site-settings.png)

    默认情况下，通过端口 80 访问 SharePoint Web 应用程序。 这意味着，通常可以通过输入访问 SharePoint 站点*http://<computer name> *以打开根网站集。

3. 在**网站集管理**，选择**网站集功能**。

4. 向下页面，直至你找到滚动**报表查看器 Web 部件**功能。

5. 选择**激活**。

    ![激活报表查看器 Web 部件功能](media/web-part-activiate-feature.png)

6. 对于其他网站集重复通过打开每个站点并单击站点操作。

（可选） 你还可用于 PowerShell 上使用的所有站点启用此功能[Enable-spfeature](https://technet.microsoft.com/library/ff607803.aspx) cmdlet。

```
Get-SPWebApplication "<web application url>" | Get-SPSite -Limit ALL | 
        ForEach-Object {
            Write-Host "Enabling feature for $($_.URL)"
            Enable-SPFeature -identity "ReportViewerWebPart" -URL $_.URL -ErrorAction Continue
        }
```

## <a name="remove-the-solution"></a>删除解决方案

尽管 SharePoint 管理中心提供解决方案收回，但你无需收回**ReportViewerWebPart.wsp**文件除非你在系统地排除安装或修补程序部署问题。

1. 在 SharePoint 管理中心内，在**系统设置**，选择**管理场解决方案**。

2. 选择**ReportViewerWebPart.wsp**。

3. 选择收回解决方案。

### <a name="remove-the-web-part-from-site-settings"></a>从站点设置中删除 web 部件

收回解决方案不会从 SharePoint 站点中的 web 部件的列表中删除报表查看器 web 部件。 若要删除报表查看器 web 部件，执行以下操作。

1. 在 SharePoint 网站上，选择**齿轮**图标在左上角，选择 **站点设置*。

    ![从齿轮图标的站点设置。](media/sharepoint-site-settings.png)

    默认情况下，通过端口 80 访问 SharePoint Web 应用程序。 这意味着，通常可以通过输入访问 SharePoint 站点*http://<computer name> *以打开根网站集。

2. 下**Web 设计器库**，选择**Web 部件**。

3. 选择**编辑图标**旁边**ReportViewerNativeMode.dwp**。 它可能不会在结果的第一页上列出。

4. 选择**删除项**。

    ![编辑和删除本机模式的报表查看器 web 部件](media/report-viewer-native-mode-edit-delete.png)

可以通过使用 PowerShell，尝试删除的 web 部件但没有为其直接命令。 有关脚本示例，请参阅[如何从 Web 部件库中删除 Web 部件](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f)。

## <a name="next-steps"></a>后续步骤

在报表查看器 web 部件已部署和激活之后, 可以将 web 部件添加到 SharePoint 页中。 有关详细信息，请参阅[添加报表查看器 web 部件连接到 SharePoint 页](add-report-viewer-web-part-to-page.md)。

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
