---
title: "安装 SQL Server Reporting Services |Microsoft 文档"
ms.date: 10/10/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 52c2f8fae79884b025e067b7d628cd3154ba93f4
ms.openlocfilehash: 5ce83ff18d6908441a3eaaf05599068ec5876308
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

---
# <a name="install-sql-server-reporting-services"></a>安装 SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

SQL Server Reporting Services 安装涉及用于存储报表项、 呈现报表和处理订阅和其他报表服务的服务器组件。  了解如何安装 Power BI 报表服务器。

若要下载 SQL Server 自 2017 年 Reporting Services，请转到[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55252)。

> [!NOTE]
> 是否在寻找 Power BI 报表服务器？ 请参阅[安装 Power BI 报表服务器](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/)。

## <a name="before-you-begin"></a>开始之前

安装 Reporting Services 之前，请查看[安装 SQL Server 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。

## <a name="install-your-report-server"></a>安装报表服务器

安装报表服务器是一个直截了当。 有仅几个步骤以安装文件。

> [!NOTE]
> 不需要在安装时可用的 SQL Server 数据库引擎服务器。 你将需要一个要在安装后配置 Reporting Services。

1. 查找 SQLServerReportingServices.exe 的位置和启动安装程序。

2. 选择**安装 Reporting Services**。

    ![安装 Reporting Services](media/install-reporting-services/report-server-install.png)

3. 选择一个版本以安装，然后选择**下一步**。

    ![选择版本](media/install-reporting-services/report-server-install-edition.png)

    向下，你可以选择从下拉评估或开发人员版。

    ![评估或开发人员版](media/install-reporting-services/report-server-install-edition-select.png)

    否则，你可以输入产品密钥。

4. 阅读并同意许可条款和条件，然后选择**下一步**。

5. 你需要一个可用于存储报表服务器数据库的数据库引擎。 选择**下一步**安装仅在报表服务器。

    ![不安装所需的数据库](media/install-reporting-services/report-server-install-db-engine.png)

6. 指定报表服务器的安装的位置。 选择**安装**以继续。

    ![指定安装路径](media/install-reporting-services/report-server-install-file-path.png)

    > [!NOTE]
    > 默认路径为 C:\Program Files\Microsoft SQL Server Reporting Services。

7. 在成功安装后选择**配置报表服务器**以启动 Reporting Services 配置管理器。

    ![配置报表服务器](media/install-reporting-services/report-server-install-configure.png)

## <a name="configuration-your-report-server"></a>配置报表服务器

选择后**配置报表服务器**在安装程序，你将看到与**报表服务器配置管理器**。 有关详细信息，请参阅[报表服务器配置管理器](reporting-services-configuration-manager-native-mode.md)。

你需要[创建报表服务器数据库](ssrs-report-server-create-a-report-server-database.md)以完成初始配置的 Reporting Services。 完成此步骤需要 SQL Server 数据库服务器。

### <a name="creating-a-database-on-a-different-server"></a>在不同服务器上创建数据库

如果你要在其他计算机上的数据库服务器中创建报表服务器数据库，你需要将报表服务器的服务帐户更改为数据库服务器识别的凭据。

默认情况下，报表服务器使用的虚拟服务帐户。 如果你尝试在不同服务器上创建数据库，可能会收到以下错误，正在应用连接权限步骤。

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

若要解决错误，可以向网络服务或域帐户更改服务帐户。 将服务帐户更改为网络服务适用报表服务器的计算机帐户的上下文中的权限。

有关详细信息，请参阅[配置报表服务器服务帐户](configure-the-report-server-service-account-ssrs-configuration-manager.md)。

## <a name="windows-service"></a>Windows 服务

Windows 服务创建为安装的一部分。 它显示为**SQL Server Reporting Services**。 服务名称是**SQLServerReportingServices**。

## <a name="default-url-reservations"></a>默认 URL 保留项

URL 保留项由前缀、主机名、端口和虚拟目录组成：

|组成部分|说明|
|----------|-----------------|
|前缀|默认的前缀为 HTTP。 如果你以前安装的安全套接字层 (SSL) 证书，安装程序将尝试创建使用 HTTPS 前缀的 URL 保留项。|
|主机名|默认主机名为强通配符 (+)。 它指定报表服务器接受解析为计算机上，任何主机名的指定端口上的任何 HTTP 请求包括`http://<computername>/reportserver`， `http://localhost/reportserver`，或`http://<IPAddress>/reportserver.`|
|端口|默认端口为 80。 如果你使用端口 80 以外的任何端口，你必须显式将其添加到的 URL，当在浏览器窗口中打开 web 门户。|
|虚拟目录|默认情况下，格式 ReportServer 为报表服务器 Web 服务和报表为 web 门户创建虚拟目录。 对于报表服务器 Web 服务，默认的虚拟目录为 **reportserver**。 对于 web 门户中，默认的虚拟目录是**报表**。|

完整的 URL 字符串示例如下所示：

- `http://+:80/reportserver`提供对报表服务器的访问。

- `http://+:80/reports`提供对 web 门户的访问。

## <a name="firewall"></a>防火墙

如果你正在从远程计算机访问报表服务器，你想要确保你已配置任何防火墙规则，如果存在防火墙。

你需要打开已为你的 Web 服务 URL 和 Web 门户 URL 配置的 TCP 端口。 默认情况下，将这些配置在 TCP 端口 80 上。

## <a name="additional-configuration"></a>其他配置

- 若要使用 Power BI 服务中配置集成，以便你可以将报表项固定到 Power BI 仪表板，请参阅[与 Power BI 服务集成](power-bi-report-server-integration-configuration-manager.md)。

- 若要配置为订阅处理的电子邮件，请参阅[电子邮件设置](e-mail-settings-reporting-services-native-mode-configuration-manager.md)和[电子邮件中的报表服务器的传递](../subscriptions/e-mail-delivery-in-reporting-services.md)。

- 若要配置 web 门户，以便你可以访问它的计算机上远程计算机中以查看和管理报表，请参阅[为报表服务器访问配置防火墙](../report-server/configure-a-firewall-for-report-server-access.md)和[配置报表服务器以进行远程管理](../report-server/configure-a-report-server-for-remote-administration.md).

## <a name="related-information"></a>相关信息

有关如何安装 SQL Server 2016 Reporting Services 本机模式的信息，请参阅[安装 Reporting Services 本机模式报表服务器](install-reporting-services-native-mode-report-server.md)。 有关如何在 SharePoint 集成模式下安装 SQL Server 2016 Reporting Services 的信息，请参阅[在 SharePoint 模式下安装第一个报表服务器](install-the-first-report-server-in-sharepoint-mode.md)。

## <a name="next-steps"></a>后续步骤

与报表服务器安装，开始创建报表并将其部署到报表服务器。 有关如何使用报表生成器启动的信息，请参阅[Install Report Builder](../../reporting-services/install-windows/install-report-builder.md)。

若要创建报表使用 SQL Server Data Tools，[下载 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714)。

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
