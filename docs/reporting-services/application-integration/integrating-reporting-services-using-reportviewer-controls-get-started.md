---
title: "ReportViewer 2016 控件入门 | Microsoft Docs"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: dff598efce33f778359c2b6fb4c3a0184f2b88f6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="integrating-reporting-services-using-reportviewer-controls---get-started"></a>使用 ReportViewer 控件集成 Reporting Services - 入门

了解开发者如何通过 Reporting Services 2016 ReportViewer 控件在 ASP.NET 网站、Windows 窗体应用中嵌入分页报表。 可向新项目添加控件，或更新现有项目。

## <a name="adding-the-reportviewer-control-to-a-new-web-project"></a>向新的 Web 项目添加 ReportViewer 控件

1. 创建新的 ASP.NET 空网站或打开现有的 ASP.NET 项目。

    ![ssRS-Create-New-ASPNET-Project](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. 通过 NuGet 包管理器控制台安装 ReportViewer 2016 控件 NuGet 包。

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. 向项目添加新的 .aspx 页并注册 ReportViewer 控件程序集供页面内使用。

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. 向页面添加 ScriptManagerControl。

5. 向页面添加 ReportViewer 控件。 可更新下面的代码段，以引用远程报表服务器上承载的报表。

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
最终页面应如下所示。

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <meta http-equiv="X-UA-Compatible" content="IE=edge" /> 
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <asp:ScriptManager runat="server"></asp:ScriptManager>        
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
            <ServerReport ReportServerUrl="http://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>

```

## <a name="updating-an-existing-project-to-use-the-reportviewer-control"></a>更新现有项目，以使用 ReportViewer 控件

若要在现有项目中使用 ReportViewer 2016 控件，请通过 Nuget 添加控件并将程序集引用更新到 14.0.0.0 版。 这包括更新项目的 web.config 和引用 ReportViewer 控件的所有 .aspx 页。

### <a name="sample-webconfig-changes"></a>示例 web.config 更改

```
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  http://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5.2">
      <assemblies>
        <!-- All assemblies updated to version 14.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 14.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.5.2"/>
    <httpHandlers>
      <!-- Version updated to 14.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 14.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>示例 .aspx

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-reportviewer-control-to-a-new-windows-forms-project"></a>向新的 Windows 窗体项目添加 ReportViewer 控件

1. 创建新的 Windows 窗体应用程序或打开现有的项目。

    ![ssRS-Create-New-winforms-Project](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. 通过 NuGet 包管理器控制台安装 ReportViewer 2016 控件 NuGet 包。

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. 通过代码添加新控件或[向工具箱添加控件](##adding-control-to-visual-studio-toolbar)。

    ```
    private Microsoft.Reporting.WinForms.ReportViewer reportViewer1;
    
    private void InitializeComponent()
    {
        this.reportViewer1 = new Microsoft.Reporting.WinForms.ReportViewer();
        this.SuspendLayout();
        // 
        // reportViewer1
        // 
        this.reportViewer1.Location = new System.Drawing.Point(168, 132);
        this.reportViewer1.Name = "reportViewer1";
        this.reportViewer1.ServerReport.BearerToken = null;
        this.reportViewer1.Size = new System.Drawing.Size(396, 246);
        this.reportViewer1.TabIndex = 0;
        // 
        // Form1
        // 
        this.Controls.Add(this.reportViewer1);
    }
    ```

## <a name="how-to-set-100-height-on-the-report-viewer-2016-control"></a>如何在 Report Viewer 2016 控件上设置 100% 高度

新的 Report Viewer 2016 控件针对 HTML5 标准模式页进行了优化，适用于所有新式浏览器。 过去使用旧的 RVC 控件设置 100% 高度属性时，即使没有任何上级指定高度，也能正常运行。 在 HTML5 中，此行为已更改。 对新的 RVC 控件设置此属性时，只有父元素具有定义的高度时，才会正常运行，即它不是自动值，或者 RVC 的所有上级也都有 100% 高度。

下面两个例子均可执行该操作。

### <a name="by-setting-the-height-of-all-the-parent-elements-to-100"></a>将所有父元素的高度设为 100%

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <style>
        html,body,form,#div1 {
            height: 100%; 
        }
    </style>
   </head>
<body>
    <form id="form1" runat="server">
    <div id="div1" >
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

### <a name="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control"></a>对 reportviewer 控件的父级设置样式高度属性

有关视区百分比长度的详细信息，请参阅[视区百分比长度](https://www.w3.org/TR/css3-values/#viewport-relative-lengths)。

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
</head>
<body>
    <form id="form1" runat="server">
    <div style="height:100vh;">
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

## <a name="adding-control-to-visual-studio-toolbar"></a>向 Visual Studio 工具栏添加控件

报表查看器控件现作为 NuGet 包提供。 因此，默认情况下，Visual Studio 工具箱不会显示报表查看器控件。 通过执行以下操作可以向工具箱添加控件。

1. 安装适用于上述 WinForms 或 WebForms 的 NuGet 包。

2. 删除工具箱中列出的 ReportViewer 控件。 这是 12.x 版的控件。

    ![ssRS-remove-old-rvcontrol-toolbox](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. 在工具箱中的任意位置单击右键，再选择“选择项...”。

    ![ssRS-toolbox-choose-item](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. 在 .NET Framework 组件中，选择“浏览”。

    ![ssRS-toolbox-browse](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. 从安装的 NuGet 包中选择“Microsoft.ReportViewer.WinForms.dll”或“Microsoft.ReportViewer.WebForms.dll”。

    > [!NOTE] 
    > NuGet 包将安装在项目的解决方案目录中。 dll 的路径将如下所示：`{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` 或 `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`。

6. 新控件将在工具箱内显示。 然后，如果需要，可将其移到工具箱内的其他选项卡中。

    ![ssRS-toolbox-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

### <a name="things-to-be-aware-of"></a>注意事项

- 此操作将在当前项目内添加一个对已安装 NuGet 包的引用。 工具箱中的项将保存到其他项目。 在新的解决方案/项目中安装 NuGet 包时，工具箱项可能引用较旧版本。 

- 即便程序集不再可用，控件仍将保留在工具箱中。 如果已删除该项目，当你尝试从工具箱中添加控件时，Visual Studio 会引发错误。 要更正此错误，请从工具箱中删除控件，并使用上述步骤重新添加。


## <a name="common-issues"></a>常见问题
    
- ReportViewer 2016 控件专用于新式浏览器。 如果浏览器在 IE 兼容性模式下呈现网页，则控件可能无法正常运行。 Intranet 站点可能需要元标记来替代鼓励在兼容性模式下呈现 Intranet 网页的设置。

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="providing-feedback"></a>提供反馈

请在 [Reporting Services MSDN 论坛](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices)上或通过向 [RVCFeedback@microsoft.com](mailto:RVCFeedback@microsoft.com) 发送电子邮件，告知团队你遇到的关于控件的问题。

## <a name="see-also"></a>另请参阅

[2016 ReportingViewer 控件中的数据收集](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)

