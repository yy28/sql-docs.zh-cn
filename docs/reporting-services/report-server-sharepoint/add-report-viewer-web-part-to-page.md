---
title: "将报表查看器 web 部件添加到 SharePoint 页 |Microsoft 文档"
ms.custom: Add the Report Viewer web part to a page within your SharePoint site.
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
ms.openlocfilehash: 033d8092cab4e6aa0889f153d5e2e7d75ae31b03
ms.contentlocale: zh-cn
ms.lasthandoff: 09/15/2017

---

# <a name="add-report-viewer-web-part-to-a-sharepoint-page"></a>将报表查看器 web 部件添加到 SharePoint 页

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

通过将报表查看器 web 部件添加到 SharePoint 页中显示的报表，从 SQL Server Reporting Services 或 Power BI 报表服务器。

![在 SharePoint 页上报表查看器 web 部件](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="prerequisites"></a>先决条件

* 为了成功加载报表，Claims to Windows Token Service (C2WTS) 需要配置 kerberos 约束委派。 有关如何配置 C2WTS 的详细信息，请参阅[Claims to Windows Token Service (C2WTS) 和 Reporting Services](../install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)。

* 必须将报表查看器 web 部件部署到你的 SharePoint 场。 有关如何部署报表查看器 web 部件解决方案项目的信息，请参阅[部署报表查看器 web 部件在 SharePoint 站点上的](deploy-report-viewer-web-part.md)。

## <a name="add-web-part"></a>添加 web 部件

1. 在 SharePoint 网站上，选择**齿轮**在左上角，选择图标**添加页**。

    ![添加到 sharepoint 站点的页，从齿轮图标。](media/sharepoint-add-a-page.png)

2. 为你的页面，指定名称和选择**创建**。

3. 在页设计器中，选择**插入**中功能区选项卡。 然后选择**Web 部件**内**部件**部分。

    ![从 office 功能区插入 web 部件。](media/sharepoint-insert-web-part.png)

4. 下**类别**，选择 * * SQL Server Reporting Services （本机模式）。 下**部件**，选择**报表查看器**。 然后选择**添加**。

    ![添加报表查看器 Web 部件。](media/sharepoint-report-viewer-web-part.png)

    出现错误，这可能最初会出现。 错误是因为默认报表服务器 URL 设置为*http://localhost*和在该位置可能不可用。

## <a name="configure-the-report-viewer-web-part"></a>将报表查看器 web 部件配置

若要配置 web 部件指向特定报表，执行以下操作。

1. 在编辑时的 SharePoint 页面，选择右上方的 web 部件的向下箭头，然后选择**编辑 Web 部件**。

    ![编辑 web 部件下拉列表中的网页。](media/sharepoint-edit-web-part.png)

2. 输入**报表服务器 URL**为承载您的报表的报表服务器。 这看起来应该类似*http://myrsserver/reportserver*。

3. 输入的路径和你想要 web 部件中显示的报表的名称。 这类似于*AdventureWorks Sample Reports/Company Sales*。 在此示例中，报表*Company Sales*位于名为的文件夹中*AdventureWorks 示例报表*。

4. 如果您的报表需要参数，提供报表服务器 URL 和报表的名称后，选择**负载参数**内**参数**部分。

5. 选择**确定**若要将所做的更改保存到 web 部件配置。

6. 选择**保存**，在 Office 功能区中，若要将所做的更改保存到 SharePoint 页中。

![在 SharePoint 页上报表查看器 web 部件](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="considerations-and-limitations"></a>注意事项和限制

* 在 SharePoint 中的现代页上，不能使用报表查看器 web 部件。
* Power BI 报表不能与报表查看器 web 部件使用。
* 如果看不到报表查看器 web 部件，将添加到你的页面，请确保你具有[部署报表查看器 web 部件](deploy-report-viewer-web-part.md)。
* 在 web 部件的顶部的链接将产生一个错误，并不导航你任意位置。

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
