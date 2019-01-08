---
title: 浏览使用 Azure 资源浏览器的 Azure SQL 资源
titleSuffix: Azure Data Studio
description: 了解如何浏览和管理 Azure SQL Server、 Azure SQL 数据库和通过 Azure 资源浏览器的 Azure SQL 托管实例。
ms.custom: seodec18
author: yanancai
ms.author: yanacai
manager: craigg
ms.date: 09/24/2018
ms.topic: quickstart
ms.prod: sql
ms.technology: azure-data-studio
ms.openlocfilehash: d202a305468f78cf1890533292570ebb56edff12
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030111"
---
# <a name="explore-and-manage-azure-sql-resources-with-azure-resource-explorer"></a>浏览和管理 Azure SQL 资源与 Azure 资源浏览器

在本文档中，您学习如何浏览和管理 Azure SQL Server、 Azure SQL 数据库和通过 Azure 资源浏览器中的 Azure SQL 托管实例资源[!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]。

>[!NOTE]
>将在 SQL Server 2019 年 10 月预览版支持 Azure 资源浏览器。 之后，可以安装通过预览扩展[扩展管理器](extensions.md)或通过**文件** > **VSIX 包从安装包**。


## <a name="connect-to-azure"></a>连接到 Azure

安装 SQL 预览插件之后, Azure 图标的左侧的菜单栏中显示。 单击该图标可以打开 Azure 资源浏览器。 如果看不到的 Azure 图标，右键单击左侧的菜单栏中，然后选择**Azure 资源浏览器**。

### <a name="add-an-azure-account"></a>添加 Azure 帐户

若要查看与 Azure 帐户关联的 SQL 资源，必须首先添加到帐户[!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]。

1. 打开**链接的帐户**通过帐户管理图标上靠左下对齐，或通过对话框**登录到 Azure...** Azure 资源浏览器中的链接。

    ![登录到 Azure](media/azure-resource-explorer/sign-in-to-azure.png)

2. 在中**链接的帐户**对话框中，单击**添加帐户**。

    ![添加 Azure 帐户](media/azure-resource-explorer/add-an-azure-account.png)

3. 单击**复制并打开**打开浏览器进行身份验证。

    ![浏览器中打开身份验证页面](media/azure-resource-explorer/open-authentication-in-browser.png)

4. 粘贴**用户代码**在网页上单击**继续**进行身份验证。

    ![在浏览器中进行身份验证](media/azure-resource-explorer/authenticate-in-browser.png)

5. 在中[!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]应会显示已登录 Azure 帐户中**链接帐户**对话框。

    ![登录 Azure 帐户](media/azure-resource-explorer/signed-in-azure-account.png)

### <a name="add-more-azure-accounts"></a>添加更多的 Azure 帐户

中支持多个 Azure 帐户[!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]。 若要添加更多的 Azure 帐户，请单击右上角的按钮**链接帐户**对话框并遵循使用的相同步骤添加一个 Azure 帐户部分以添加更多的 Azure 帐户。

![添加更多的 Azure 帐户](media/azure-resource-explorer/add-more-azure-account.png)

### <a name="remove-an-azure-account"></a>删除 Azure 帐户

若要删除的现有登录 Azure 帐户：

1. 打开**链接帐户**对话框通过左下角的帐户管理图标。
2. 单击**X**按钮右侧的 Azure 帐户以将其删除。

    ![删除 Azure 帐户](media/azure-resource-explorer/remove-azure-account.png)

## <a name="filter-subscription"></a>筛选器订阅

登录到 Azure 帐户，与该 Azure 帐户显示在 Azure 资源浏览器相关联的所有订阅。 您可以筛选每个 Azure 帐户的订阅。

1. 单击**选择订阅**按钮右侧的 Azure 帐户。

   ![筛选器订阅](media/azure-resource-explorer/filter-subscription.png)

2. 选择你想要浏览，然后单击帐户订阅的复选框**确定**。

   ![选择订阅](media/azure-resource-explorer/select-subscription.png)

## <a name="explore-azure-sql-resources"></a>浏览 Azure SQL 资源

若要导航的 Azure SQL 资源在 Azure 资源浏览器中，展开 Azure 帐户和组资源类型。

Azure 资源浏览器支持目前支持 Azure SQL Server、 Azure SQL 数据库和 Azure SQL 托管实例。

## <a name="connect-to-azure-sql-resources"></a>连接到 Azure SQL 资源

Azure 资源浏览器提供可帮助你连接到 SQL 服务器和数据库的查询和管理的快速访问。 

1. 了解你想要使用连接的树视图中的 SQL 资源。
2. 右键单击该资源，然后选择**Connect**，还可以找到连接按钮右侧的资源。

   ![连接到 Azure SQL 资源](media/azure-resource-explorer/connect-to-azure-sql-resource.png)

3. 在中打开**连接**对话框中，输入你的密码，然后单击**Connect**。

   ![SQL 连接对话框](media/azure-resource-explorer/sql-connection-dialog.png)
4. **服务器**窗口会自动打开与新连接的 SQL 服务器/数据库连接成功后。

## <a name="next-steps"></a>后续步骤

- [使用[!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)]进行连接和查询 Azure SQL 数据库](quickstart-sql-database.md)
- [使用[!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)]进行连接和查询 Azure SQL 数据仓库中的数据](quickstart-sql-dw.md)