---
title: "开始使用 ReportViewer 2016 控件 |Microsoft 文档"
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
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 71ca2fac0a6b9f087f9d434c5a701f5656889b9e
ms.openlocfilehash: 51c6e0a0baa59e49ae482db01253c1998894b5f8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/13/2017

---
# <a name="integrating-reporting-services-using-reportviewer-controls---get-started"></a>将集成 Reporting Services 使用 ReportViewer 控件-入门

了解如何开发人员可以将分页的报表嵌入在 ASP.NET web 站点和 Windows 窗体应用程序，通过 Reporting Services 2016 ReportViewer 控件中。 你可以将控件添加到新项目，或更新现有项目。

## <a name="adding-the-reportviewer-control-to-a-new-web-project"></a>将 ReportViewer 控件添加到新的 web 项目

1. 创建一个新**ASP.NET 空网站**或打开现有的 ASP.NET 项目。

    ![ssRS 创建的新-ASPNET 的项目](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. 安装 ReportViewer 2016 控件 nuget 包通过**Nuget 包管理器控制台**。

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. 向项目添加一个新的.aspx 页面，并注册页中使用的 ReportViewer 控件程序集。

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. 添加**ScriptManagerControl**到页。

5. 将 ReportViewer 控件添加到页。 可以更新下面的代码段以引用的远程报表服务器上托管的报表。

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
最后一页应如下所示。

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

## <a name="updating-an-existing-project-to-use-the-reportviewer-control"></a>更新现有项目以使用 ReportViewer 控件

要使用的现有项目中的 ReportViewer 2016 控件、 添加通过 Nuget 控件和更新版本的程序集引用*14.0.0.0*。 这将包括更新项目的 web.config 和所有引用 ReportViewer 控件的.aspx 页。

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

### <a name="sample-aspx"></a>示例.aspx

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-reportviewer-control-to-a-new-windows-forms-project"></a>将 ReportViewer 控件添加到新的 Windows 窗体项目

1. 创建一个新**Windows 窗体应用程序**或打开现有项目。

    ![ssRS 创建的新的 winforms 的项目](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. 安装 ReportViewer 2016 控件 nuget 包通过**Nuget 包管理器控制台**。

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. 从代码中添加新控件或[将控件添加到工具箱](##adding-control-to-visual-studio-toolbar)。

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

## <a name="how-to-set-100-height-on-the-report-viewer-2016-control"></a>如何在报表查看器 2016年控件上设置 100%高度

新的报表查看器 2016年控件针对 HTML5 标准模式页进行了优化，并可用于所有现代浏览器。 在过去，与旧的 RVC 控件，当你设置 100 %height 属性，它的工作即使无上级具有指定的高度。 此行为已更改 html5 格式。 当新 RVC 控件上设置此属性时，它将正常工作的父元素有一个定义的高度才，即不是值的自动或所有祖先构成的 RVC 太具有 100%的高度。

以下是两个示例，以执行此操作。

### <a name="by-setting-the-height-of-all-the-parent-elements-to-100"></a>通过将所有父的高度设置为 100%的元素

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

### <a name="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control"></a>通过在 reportviewer 控件的父类上设置样式高度属性

视区百分比长度有关的详细信息，请参阅[视区百分比长度](https://www.w3.org/TR/css3-values/#viewport-relative-lengths)。

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

## <a name="adding-control-to-visual-studio-toolbar"></a>将控件添加到 Visual Studio 工具栏

报表查看器控件现在提供作为 NuGet 程序包。 因此，你将不看到默认情况下显示在 Visual Studio 工具箱报表查看器控件。 通过执行以下，可以将控件添加到工具箱。

1. WinForms 或 WebForms 上文所述安装 NuGet 包。

2. 工具箱中删除列出的 ReportViewer 控件。 这是使用版本 12.x 的控件。

    ![ssRS-删除的旧-rvcontrol-工具箱](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. 右键单击在任何地方工具箱中，然后选择**选择项...**.

    ![ssRS 工具箱-选择的项](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. 上**.NET Framework 组件**，选择**浏览**。

    ![ssRS 工具箱浏览](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. 选择**Microsoft.ReportViewer.WinForms.dll**或**Microsoft.ReportViewer.WebForms.dll**从你安装了 NuGet 程序包。

    > [!NOTE] 
    > 将你的项目的解决方案目录中安装 NuGet 包。 Dll 的路径将类似于以下：`{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40`或`{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`。

6. 新的控件应显示在工具箱中。 你可以将其移动到另一个选项卡，工具箱中如果你想。

    ![ssRS 工具箱 rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

### <a name="things-to-be-aware-of"></a>需要注意的事项

- 这将添加到当前项目中已安装的 NuGet 程序包的引用。 工具箱中的项将保存到其他项目。 在新的解决方案/项目中安装 NuGet 包时，工具箱项可能引用较旧版本。 

- 控件将保留在工具箱中，即使该程序集不再不可用。 如果已删除该项目，Visual Studio 将引发错误，如果你尝试并从工具箱中添加控件。 若要更正此错误，从工具箱中删除控件，然后重新添加使用上述步骤。


## <a name="common-issues"></a>常见的问题
    
- ReportViewer 2016 控件设计用于现代浏览器。 如果浏览器呈现在 IE 兼容性模式下的网页，该控件可能不正常。 Intranet 站点可能需要一个元标记可替代设置的鼓励呈现在兼容模式下的 intranet 页。

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="providing-feedback"></a>提供反馈

让团队了解有关你遇到与该控件的问题[Reporting Services MSDN 论坛](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices)或通过电子邮件在[ RVCFeedback@microsoft.com ](mailto:RVCFeedback@microsoft.com)。

## <a name="see-also"></a>另请参阅

[2016 ReportingViewer 控件中的数据收集](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)


